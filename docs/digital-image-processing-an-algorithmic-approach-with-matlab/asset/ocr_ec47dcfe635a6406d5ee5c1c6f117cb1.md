```
```
DF = zeros(r,c) ;
DFF = DF ;
IDF = DF ;
IDFF = DF ;
depth = 4 ;
N = 8 ;
for i = 1 : N : r
  for j = 1 : N : c
    f = x(i:i+N-1,j:j+N-1) ;
    df = dct2(f) ;
    DF(i:i+N-1,j:j+N-1) = df ;
    dff = idct2(df) ;
    DFF(i:i+N-1,j:j+N-1) = dff ;
    df (N-1:depth-1,:) = 0 ;
    df(:,N-1:depth-1) = 0 ;
    IDF (i:i+N-1,j:j+N-1) = df ;
    dff = idct2(df) ;
    IDFF(i:i+N-1,j:j+N-1) = dff ;
  end
end
figure
imshow(DF)
figure
imshow(DFF*0.005)
figure
imshow(IDF)
figure
imshow(IDFF*0.004)
```
```

# 8.10 SUMMARY

+   - Image compression refers to the technique in which image pixel values are mapped into a data space from where they can be stored using a more compact structure.
+   - The first level of mapping usually comprises some type of transformation from pixel domain to coefficient domain of some type.
+   - These coefficients are then quantized in magnitude as well as in terms of their locations.