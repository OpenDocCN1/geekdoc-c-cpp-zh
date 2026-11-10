```
```matlab
I = imread('Image1','jpeg');
flg=isrgb(I);

if flg==1
    I=rgb2gray(I);
end

[h,w]=size(I);
figure;imshow(I);

c = edge(I, 'canny',0.3);       % Mcanny edge
detection
figure; imshow(c);              % binary edges

se = strel('disk',2);            %
I2 = imdilate(c,se);              %
imshow(I2);                       %

d2 = imfill(I2, 'holes');         %
figure, imshow(d2);               %

Label=bwlabel(d2,4);

a1=(Label==1);
a2=(Label==2);
a3=(Label==3);
a4=(Label==4);
a5=(Label==5);
a6=(Label==6);

D1 = bwdist( a1); % computing minimal euclidean
                  % distance to non-white pixel
figure, imshow(D1,[]);
[xc1 yc1 r1]=merkk(D1);
f1=coinDetect(r1)
```
```