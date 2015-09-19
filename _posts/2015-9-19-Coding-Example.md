---
layout: post
title: Know your language -- how to get best of programming language
tag: C, Matlab, GPS
category: coding
---

I created this blog with the main goal of describing my experience with Big Data. I have started to actively learning it nine months ago, by doing Cursera courses and participating in a [competition on Kaggle](https://www.kaggle.com/c/seizure-prediction). And I have just completed [Science to Data Science](http://www.s2ds.org/) course, allowing me to pull toghether all this knowledge in the practical project (more about it in later post, but if you are impatient my team mate Lin, [already blogged about it](http://linbug.github.io/data%20science/2015/09/10/Takeaways-from-S2DS/)).


![GPS Satellite](https://en.wikipedia.org/wiki/File:GPS-IIRM.jpg)


One interesting insight that transposed from those events is the importance of knowing programming language and knowing it well. Quite a while back, while enjoying early stage of my PhD, a fellow sufferer discussed with me a code he was working on in C. Both of us worked on GPS related issues and code was generating [replica pseduo-random code](http://www.trimble.com/gps_tutorial/sub_pseudo.aspx). In brief, this is required by the receiver to decode incoming message from the specific satellite in order to decode distance (psuedorange) which allows received to provide the position. GPS is utilising [Gold Codes](https://en.wikipedia.org/wiki/Gold_code) famous for low cross-correlation.

This code was intend to run in real time and hence written in C. We have been both toying with Matlab at the time and my colleague invented a challenge -- can I  write a Matlab code matching in speed following pseudo random code generator from C? At this stage I was just off fresh from reading [Pascal Getreuer's notes about Matlab vectorisation](http://www.getreuer.info/matopt.pdf) and decide to take a challenge. It was 16:00 and I proudly boasted to finish within 1h. It was not until 21:00 when I completed the code below, which runs only 2% slower then original C code. 

What is the most interesting takeaway is that both of us benefited from this exercise. I gained much better understanding of Matlab, demonstrated my understanding of matrices but also understood how much less readable is production code from exploratory one. My friend used my example to re-write his original C code, which was subsequently implemented in commercial product. 


I attached both codes below.

```Matlab

function [rep_code] = GenerateReplicaCode(n, sample_freq, freq, offset, key)

%
% Generate the replica code signal for a given PRN aligned with
% time signal t, of frequency freq and initial offset (chips) of
% offset.
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

I based my Matlab implementation on the C code below. It is worth noticing that C code is using loop and hence is slow, it was subsequently tuned for high speed using some of the ideas that steamed from my Matlab implementation.


```C
#include "mex.h"

/* function [rep_code] = GenerateReplicaCode(n, sample_freq, freq, offset, key) */

/*
% Generate the replica code signal from the supplied key aligned with
% time signal t (n elements long), of frequency freq and initial offset 
% (chips) of offset.
%
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
