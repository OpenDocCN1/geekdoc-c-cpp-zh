![](bbox=[0.33, 0.08, 0.66, 0.56])

# FIGURE 5.9 Algorithm for Hough transform.

```
figure ; imshow(YG*0.0001)
figure ; imshow(YB*0.0001)
% Grayscale FFT (Figure 5.2)
xg = rgb2gray(x) ;
figure ; imshow(xg) ;
XG = fft2(xg,1024,1024) ;
XGM=(abs(XG)) ;
figure ; imshow(XGM*0.00005) ;
XGMS = fftshift(XGM) ;
figure ; imshow(XGMS*0.00005) ;
%Effect of Rotation (Figure 5.2)
xr = imrotate(xg,30) ; %rotation by 30 degrees
figure ; imshow(xr) ;
XR = fft2(xr,1024,1024) ;
```