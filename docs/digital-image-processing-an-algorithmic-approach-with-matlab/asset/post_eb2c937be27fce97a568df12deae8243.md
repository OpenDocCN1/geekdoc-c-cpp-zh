
![](img/fc093ca9cc8a631842aa559a749dca54_139_0.png)

FIGURE 6.10 Case-based spatial filtering. (a) Median filtering, (b) conservative filtering.

maximum values of the eight neighbors of the central pixel, and decide on the replacement criteria. These two case-based filters can be thought of as the algorithms shown in Figure 6.10.

## 6.4.3 Frequency Filtering

Frequency filtering works very similarly to the spatial filtering shown in Figure 6.9, except for the image transformation steps in the beginning and end of the algorithm and replacement of convolution with multiplication. This is shown in Figure 6.11.

## 6.5 MATLAB® CODE

In this section, the MATLAB code used to generate the images in Figures 6.2, 6.3, 6.4, 6.6, 6.7, and 6.8 is presented. Except for Figures 6.7 and 6.8, all other listed figures are covered in the following code:

```
close all
clear all

h1 = ones(3)/9 ;
```

![](img/fc093ca9cc8a631842aa559a749dca54_140_0.png)

FIGURE 6.11 Frequency filtering algorithm.

```
h2 = fspecial('gaussian',5,5);
x=imread('sr71.jpg');
x = rgb2gray(x);
figure ; imshow(x)
% Gaussian Noise
xng = imnoise(x,'gaussian',0,0.1);
figure ; imshow(xng)
g1 = imfilter(xng,h1);
figure ; imshow(g1)
g2 = imfilter(xng,h2);
figure ; imshow(g2)
g3 = medfilt2(xng) ;
figure ; imshow(g3)
g4 = conserv(xng) ;
figure ; imshow(g4*0.003)
```

### Salt & Pepper Noise

```
xns = imnoise(x,'salt & pepper',0.1);
figure ; imshow(xns)
g5 = imfilter(xns,h1);
figure ; imshow(g5)
g6 = imfilter(xns,h2);
figure ; imshow(g6)
g7 = medfilt2(xns) ;
figure ; imshow(g7)
g8 = conserv(xng);
figure ; imshow(g8*0.003)
```

The function conserv does not exist in MATLAB and was coded as follows:

```
function y1 = conserv(xng)
[r,c] = size(xng) ;
x1 = zeros(r+2,c+2) ;
x1(2:r+1,2:c+1) = xng ;
[r,c] = size(x1) ;
y1 = x1 ;

for i = 2 : r-1
    for j = 2 : c-1
        nh = [x1(i-1,j-1) x1(i-1,j) x1(i-1,j+1)
        x1(i,j-1) x1(i,j+1) x1(i+1,j-1) x1(i+1,j)
        x1(i+1,j+1)] ;
        cp = x1(i,j) ;
        mx = max(nh) ; mn = min(nh) ;
        if (cp > mx), cp = mx ;
        else if (cp < mn), cp = mn ;
        end
        end
        y1(i,j)= cp ;
    end
end
return
```

The following code is for Figures 6.7 and 6.8:

```
close all
clear all

h1 = ones(3)/9 ;
h2 = fspecial('gaussian',5,5);
H1 = fft2(h1, 1024,1024) ;
H2 = fft2(h2, 1024,1024) ;
figure ; mesh(fftshift(real(H1)))
figure ; mesh(fftshift(real(H2)))
figure ; imshow(fftshift(abs(H1))*20)
figure ; imshow(fftshift(abs(H2))*20)
```

```
x=imread('sr71.jpg');
x = rgb2gray(x) ;
[r,c] = size(x);

% Gaussian Noise
xng = imnoise(x,'gaussian',0,0.1);
figure ; imshow(xng)
XNG = fft2(xng,1024,1024) ;
figure ; imshow(fftshift(abs(XNG))*0.00001)
G1 = XNG .* H1 ;
g1 = ifft2(G1) ;
g1 = g1(1:r,1:c) ;
figure ; imshow(g1*0.004)
G2 = XNG .* H2 ;
g2 = ifft2(G2) ;
g2 = g2(1:r,1:c) ;
figure ; imshow(g2*0.004)
```

```
% Salt & Pepper Noise
xns = imnoise(x,'salt & pepper',0.1);
figure ; imshow(xns)
XNS = fft2(xns,1024,1024) ;
figure ; imshow(fftshift(abs(XNS))*0.00001)
G3 = XNS .* H1 ;
g3 = ifft2(G3) ;
g3 = g3(1:r,1:c) ;
figure ; imshow(g3*0.004)
G4 = XNS .* H2 ;
g4 = ifft2(G4) ;
g4 = g4(1:r,1:c) ;
figure ; imshow(g4*0.004)
```

## 6.6 SUMMARY

- Filtering is the operation of removing certain frequency components from an image.
- Image filters can work directly in the spatial domain as well as in the frequency domain.
- In the spatial domain, the filter can be thought of as a small M × N matrix, called kernel or mask, that is convolved with the source image.
- In such a convolution operation, a small neighborhood in the image (proportional to the kernel) is operated on, and a new pixel value is obtained as the corresponding center pixel of the neighborhood.
- For the case of boundaries, additional rows and columns are added that are either replicas of the outer rows and columns or just zeros (zero padding).
- The spatial filters can also be based on checking certain constraints within the neighborhood, so that outlier values can be smoothed out. Conservative and median filtering are two such filters.
- The images can also be processed in the frequency domain. Here, a specific mask is needed to remove or allow certain areas of the frequency spectrum.
- Noise is usually the higher frequency aspect of the image and can be removed by the low-pass filter mask, which is usually some type of circular and zero-centered mask.
- However, removing the noise frequencies also removes with them some useful high-frequency components such as edges in the image, thus producing a blurred image.
- Careful selection of the mask and its application can achieve a compromise solution in which noise removal and edge conservation are optimized.

## 6.7 EXERCISES

- 1. Apply a high-pass filter to the image in Figure 6.7(e). Reduce the power of the Gaussian noise by a factor of 4, and repeat the high-pass filtering for this less noisy image. Comment on the edge enhancement in the image in both cases. [Hint: Check the help documentation of the `fspecial()` function in MATLAB for the design of high-pass filters]

- 2. Apply a conservative filter to the image in Figure 6.6 by reducing the salt-and-pepper noise by a factor of 4. Then compare with the results in Figure 6.6.

- 3. Take a heavily noisy image, for example, Figure 6.3(a). Apply the Gaussian spatial filter of size 7 x 7. Then apply the filter obtained in Q #1 to the filtered image. Is this iterative procedure better than simple low-pass filtering? Can the iterative procedure be continued further? If so, for typically how many more times before losing significant information?

- 4. Referring to the procedure for Figure 6.8, perform the following experiment:

- a. Once the 1024 x 1024 frequency domain representation of the noisy image is obtained, use the mask shown in Figure EX6.1(a) as is to remove certain portions of the frequency domain image.

- b. Inverse-transform the resulting image to obtain the filtered spatial-domain representation of the filtered image.

- 5. Repeat Q #4 for the mask shown in Figure EX6.1(b).

![](img/fc093ca9cc8a631842aa559a749dca54_144_0.png)

![](img/fc093ca9cc8a631842aa559a749dca54_144_1.png)

FIGURE EX6.1

# Image Restoration and Blind Deconvolution

## 7.1 INTRODUCTION

IMAGE ENHANCEMENT, IN GENERAL, covers all aspects of improving image quality for visual purposes. This includes

- 1. Noise removal
- 2. Contrast stretching
- 3. Histogram equalization
- 4. Filtering
- 5. Restoration through deconvolution

All convolution-related topics have been covered in earlier chapters except image restoration and the underlying mathematics of deconvolution; these will be discussed in this chapter.

Images are produced in order to record or display useful information. No image information is perfect because of inherent physical and technological limitations. With the ever-increasing demand for improvement in the quality of digital images, there is a need to correct errors caused by the imaging system. These errors have many causes, including the hardware; insertion of additive or multiplicative noise by both human and other sources; and blurring of the image by linear motion of the imaging equipment or misalignment, causing defocusing.

One of the most intriguing questions in image processing is the problem of recovering the desired or perfect image from a degraded version. The amount of lost information that can be recovered from the blurred version of an image depends on the extent of degradation. This sets a bound on the performance of the image restoration algorithm.

In order to solve the image restoration problem, mathematical models are required for real-world processes involved in image generation, formation, and recording. It may be argued that the ultimate objective of a restoration scheme is the inverse manipulation of the degraded model into the original nondegraded model. If this task is performed based on certain statistical knowledge, known beforehand, about the degradation process, the medium, and the noise, the procedure is called a priori restoration. On the other hand, this information may not be available with a high degree of fidelity. In that case, blind restoration or blind deconvolution methodologies are adopted.

## 7.2 IMAGE REPRESENTATION

In order to understand the functioning of certain restoration techniques, the morphology of the target image and the degradation in it should be understood first. The general notation for digital images is to consider them as matrices represented in x and y coordinates. Thus, an image of interest f(m,n) is a matrix of m x n order that is the result of 2D sampling of the real image. However, the image model f(m,n) is not the observed image because of the distortion present in the imaging system. A general imaging system block diagram is shown in Figure 7.1.

Hence, the observed image g(m,n) is given by

g(m,n) = f(m,n) \circledast h(m,n) + \eta(m,n), (7.1)

![](img/fc093ca9cc8a631842aa559a749dca54_147_0.png)

FIGURE 7.1 Imaging system and its block diagram.
