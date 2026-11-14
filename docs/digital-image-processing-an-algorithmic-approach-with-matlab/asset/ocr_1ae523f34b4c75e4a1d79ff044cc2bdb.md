# 11.5 ALGORITHMIC ACCOUNT

A typical methodology for coding the watermarks is shown in Figure 11.5.

# 11.6 MATLAB® CODE

In this section, the MATLAB code used to generate the images in Figures 11.3 and 11.4 is presented.

```
clear all
close all
x = double(imread('horses.jpg'));
figure ; imshow(x*0.003) ;
y = x ;
```

![](bbox=[0.25, 0.37, 0.7, 0.82])

FIGURE 11.5 Methodology for coding watermarks. (a) Watermarking procedure, (b) dewatermarking procedure.