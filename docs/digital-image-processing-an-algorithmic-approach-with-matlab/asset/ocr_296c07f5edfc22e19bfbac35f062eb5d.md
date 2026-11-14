```
c13 = [0 130 ]; % horse
c3 = [ 255 0 255 ];
c14 = [ 221 255 ]; % water
c4 = [ 0 0 255 ] ;
[r,c] = size(xg) ;
y = x ;
for i = 1 : r
    for j = 1 : c
        if (xg(i,j) >= c11(1) && xg(i,j) <= c11(2))
            cc = c1 ;
        else
            if (xg(i,j) >= c12(1) && xg(i,j) <= c12(2))
                cc = c2 ;
            else
                if (xg(i,j) >= c13(1) && xg(i,j) <= c13(2))
                    cc = c3 ;
                else
                    cc = c4 ;
                end
            end
        end
    end
    for k = 1 : 3
        y(i,j,k) = cc(k) ;
    end
end
end
figure
imshow(y)
```

Following is the code for Figure 12.3:

```
close all
clear all
% Read the source RGB image
x = imread('horses.jpg');
figure ; imshow(x)
[r,c,s] = size(x) ;
% Initialize storage for each sample region.
classes = { 'sky','land','water','horse1','horse2' } ;
nClasses = length(classes) ;
sample_regions = false([r c nClasses]) ;
```