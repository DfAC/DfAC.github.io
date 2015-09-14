---
layout: post
title: Generating GPS SNR in C and python
tag: C, Matlab
category: coding
---

Quite a while back a friend asked me to write a Matlab code matching in speed following pseudo random code generator from C


```C
#include "mex.h"

/* function [rep_code] = GenerateReplicaCode(n, sample_freq, freq, offset, key) */

/*
% Generate the replica code signal from the supplied key aligned with
% time signal t (n elements long), of frequency freq and initial offset 
% (chips) of offset.
%
% Note that this function is extremely slow due to the use of a 
% loop - it needs to be compiled for speed, or a faster matrix
% way found to do it.
%
*/

/*
if nargin ~= 4
    error('Incorrect number of input arguments')
end

clear rep_code;

ca_code = GenerateCACode(PRN);
code_phase_step = 1 / freq;
tsz = max(size(t));
for i=1:tsz;
    idx = t(i) / code_phase_step;
    rep_code(i) = ca_code(mod(floor(idx + offset),1023) + 1);
end
*/

void GenerateReplicaCode(double rep_code[], int n, double sample_freq, double freq, double offset, int key[]) {
    int i;
    double code_phase_step = 1.0 / freq;
    double sample_period = 1.0 / sample_freq;
    for(i=0; i<n; ++i) {
        double fdx = (i * sample_period) / code_phase_step;
        rep_code[i] = key[(int)(fdx + offset) % 1023];
    }
}

/*
void timestwo(double y[], double x[])
{
  y[0] = 2.0*x[0];
}
*/

void mexFunction( int nlhs, mxArray *plhs[],
                  int nrhs, const mxArray *prhs[] )
{
    double *rep_code;
    int *key;
    int     mrows,ncols;
    int n;
    double sample_freq, freq, offset;
  
    /* Check for proper number of arguments. */
    if(nrhs!=5) {
        mexErrMsgTxt("One input required.");
    } else if(nlhs>1) {
        mexErrMsgTxt("Too many output arguments");
    }
  
    /* The input must be a noncomplex scalar double.*/
    /*
    mrows = mxGetM(prhs[0]);
    ncols = mxGetN(prhs[0]);
    if( !mxIsInteger(prhs[0]) || mxIsComplex(prhs[0]) ||
        !(mrows==1 && ncols==1) ) {
            mexErrMsgTxt("Input 1 must be a noncomplex scalar integer.");
    }
    */
    
    n = (int)(mxGetScalar(prhs[0]) + 0.5);
    sample_freq = (double)(mxGetScalar(prhs[1]));
    freq = (double)(mxGetScalar(prhs[2]));
    offset = (double)(mxGetScalar(prhs[3]));
    key = mxGetPr(prhs[4]);
    
    /* Create matrix for the return argument. */
    plhs[0] = mxCreateDoubleMatrix(1,n, mxREAL);
  
    /* Assign pointers to each input and output. */
    /*x = mxGetPr(prhs[0]);*/
    rep_code = mxGetPr(plhs[0]);
  
    /* Call the timestwo subroutine. */
    GenerateReplicaCode(rep_code, n, sample_freq, freq, offset, key);
}
```

The main question was, can Matlab code, using vectorisation from [this great guide](http://www.getreuer.info/matopt.pdf?attredirects=0) by Pascal Getreuer.
My final code looked like this

```Matlab

function [rep_code] = GenerateReplicaCode(n, sample_freq, freq, offset, key)

%
% Generate the replica code signal for a given PRN aligned with
% time signal t, of frequency freq and initial offset (chips) of
% offset.
%
% Note that this function is not longer extremely slow due to the  
% use of a Bonenberg-Luff approach
%

Key_lenght = 1023;

if nargin ~= 5
	error('Incorrect number of input arguments')
end
clear rep_code;

code_phase_step = 1 / freq;
sample_period = 1 / sample_freq;
ChangeRatio = sample_period / code_phase_step; %when chip changes

%define key offset
if (offset~=0)
    offset=mod(offset,Key_lenght);
    if (offset<0)
        offset=Key_lenght+offset;
    end
    key = [key(offset:end) key(1:offset-1)]; %offset key
end

%find all change point
ChangePoints = 1:ChangeRatio*n;
ChangePoints = ceil(ChangePoints./ChangeRatio);
ChangePoints= [ChangePoints(1) (ChangePoints(2:end)-ChangePoints(1:end-1))];

%creates full key
CodeExtractSize = size(ChangePoints,2);
LoopKey(1) = floor(mod(CodeExtractSize,Key_lenght)); %repeats of code
LoopKey(2) = CodeExtractSize-LoopKey(1)*Key_lenght; %remaining chips
rep_code = [];
if LoopKey(1)
    full_key = repmat(key,LoopKey(1),1); %copies n times 
end
if LoopKey(2)
    full_key=[rep_code key(1:LoopKey(2))]; %copies remaining chips
end

LastChip = [];
TailReading = floor((ChangeRatio*n-floor(ChangeRatio*n))/ChangeRatio); %readings after last change
if (TailReading) %check for tail
    if (LoopKey(2)+1 == Key_lenght)
        LastChip = key(end);
        LastChip = repmat(LastChip,TailReading,1);
    else
        LastChip = key(mod(LoopKey(2)+1,Key_lenght));
%         LastChip = repmat(LastChip,[TailReading,1]);
        LastChip = ones(LastChip,1).*TailReading;
    end
end

%create replica code
MaxSamples_per_key = max(ChangePoints);
rep_code = repmat(full_key,MaxSamples_per_key,1)';
%trace "skipped" chips
SkipChip = ChangePoints<MaxSamples_per_key;
rep_code(SkipChip,end) = 100; %mark for removal
rep_code=reshape(rep_code',1,[]);
%remove all "skipped" chips and add tail
rep_code = [rep_code(rep_code<100) LastChip'];


end %function

```