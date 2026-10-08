![](bbox=[0.27, 0.09, 0.81, 0.41])

# 12.7.9 Images

We can also load images from files:

```
```
Image ii {Point(100,50),"image.jpg"} ;   // 400*212-pixel jpg
win.attach(ii) ;
win.set_label("Canvas #10") ;
win.wait_for_button() ;
```
```

As it happens, the file called **image.jpg** is a photo of two planes breaking the sound barrier:

![](bbox=[0.28, 0.62, 0.81, 0.92])