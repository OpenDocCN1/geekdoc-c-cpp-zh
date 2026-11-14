![](bbox=[0.15, 0.06, 0.85, 0.45])

FIGURE 15.6 Algorithm for fuzzy clustering.

# 15.3 ALGORITHMIC ACCOUNT

The two examples presented in the previous section can be programmed according to the logic shown in Figures 15.6 and 15.7, respectively.

# 15.4 MATLAB CODE

In this section, the MATLAB code used to generate the images in Figures 15.4 and 15.5 is presented.

```
```matlab
% Unsupervised Classification with Fuzzy C-Mean
% Only input from user is the number of classes (N)
close all
clear all
N = 5 ; % Number of classes
x=imread('onion.png');
figure ; imshow(X)
```
```