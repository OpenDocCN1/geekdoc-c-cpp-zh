```
end

figure ; imshow(y)
XC = [ XC ; y ] ;
z=im2bw(y) ;
z(ro:1:ro+4, 1:co) = 255 ;
w = bwmorph(z,'erode',3) ;
Z1G = [ Z1G ; w ] ;
Z1B = [ Z1B ; z ] ;
end

figure ; imshow(X)
figure ; imshow(XC)
figure ; imshow(Z1G)
figure ; imshow(Z1B)
```

# 13.9 SUMMARY

+   • Target tracking is a very important technique used in a number of industrial and defense-related applications.
+   • The basic idea is to enhance the changes occurring in subsequent frames in a sequence of images or video.
+   • The changes usually refer to the objects of interest, including a particular target object.
+   • Many techniques have been developed for various application domains and environments.
+   • However, the fundamental technique of removing the static portions of an image such as background, etc., is part of all of these techniques.
+   • Four such fundamental techniques are presented in this chapter to track a moving artifact in an image sequence with a fixed background.
+   • The first method is used only in a scenario in which just one object is under consideration and can be extracted simply by subtracting the static background image.
+   • In the second method, in addition to background removal, temporal frames are also subtracted to track any moving object in the time interval between the frames.