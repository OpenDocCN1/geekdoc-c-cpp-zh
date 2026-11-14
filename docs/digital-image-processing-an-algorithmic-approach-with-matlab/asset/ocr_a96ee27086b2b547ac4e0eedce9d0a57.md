![](bbox=[0.13, 0.08, 0.9, 0.53])

FIGURE 8.8 Algorithm for the application of inverse DCT on an image.

# 8.9 MATLAB® CODE

In this section, the MATLAB code used to generate the images in Figures 8.1, 8.3, and 8.6 is provided. Figures 8.4 and 8.5 were also obtained from the Array editor feature of MATLAB for the variables DF and IDF.

```
close all
clear all
x=imread ( 'cameraman.tif' );
imshow(x)
F=dct2(x) ;
figure
imshow (F*0.01)
ff = idct2(F) ;
figure
imshow(ff*0.004)
[r,c] = size(x) ;
```