tools that aid in navigating around an image, especially large images, and enable the inspection of pixels in an image. Figure 1.1(a) is the result of execution of the aforementioned command imshow( ). The MATLAB code for the images in Figures 1.1-1.3 is

# 1.6.2 Sampling

```
clear all ; close all
x = imread('horses.jpg');
imshow(x)
[r,c,s] = size(x) ;
N = 10 ;
Y = zeros(size(x)) ;
y(1:N,r,1:N,c,:) = X(1:N:r,1:N:c,:) ;
z = y(1:N:r,1:N:c,:) ;
figure
imshow(z*0.005)
```

# 1.6.3 Noisy Image

```
clear all ; close all
x = imread('flowers001.jpg');
imshow(x)
[r,c,s] = size(x) ;
y = imnoise(x,'salt & pepper',0.19) ;
snr = 20*log10(sum(sum(sum(x.^2)))/
sum(sum(sum((y-x).^2)))) ;
figure
imshow(y)
```

# 1.6.4 Bit Resolution

```
clear all ; close all
x = imread('valley.jpg');
imshow(x)
[r,c,s] = size(x) ;
m = max(max(x)) ;
b = [7 6 5] ;
```