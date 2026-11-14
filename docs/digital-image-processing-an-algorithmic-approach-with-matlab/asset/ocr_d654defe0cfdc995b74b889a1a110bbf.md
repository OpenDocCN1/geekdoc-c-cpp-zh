```
```
Q = imread('testpat1.png') ;
figure ; imshow(Q)
x = 0.8 ;
R = imlincomb(x,P,1-x,Q) ;
figure ; imshow(R)
x = 0.2 ;
R = imlincomb (x,P,1-x,Q);
figure ; imshow (R)
```
```

The results from this code are shown in Figure 3.10.

![](bbox=[0.05, 0.29, 0.45, 0.55])

![](bbox=[0.48, 0.29, 0.9, 0.55])

![](bbox=[0.05, 0.57, 0.45, 0.85])

![](bbox=[0.48, 0.57, 0.9, 0.85])

FIGURE 3.10 Results of code merging two images. (a) Original image P, (b) original image Q, (c) and (d) are results of xP + (1 - x)Q for x = 0.8 and 0.2, respectively.