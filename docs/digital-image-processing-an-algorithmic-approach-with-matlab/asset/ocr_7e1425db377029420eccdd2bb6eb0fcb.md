+   - Start
+   - Load Image File (F)
+   - Initialize Convolutional kernel, image size (M,N), mask size (V), and thresholding
+   - Loop (m,n) With inc. 9
+   - Calculation of the mask with image segment in the loop with Convolution for (x,y) = 0 to V-1
+   - Threshold image segment
+   - Display Images
+   - End

+   - Start
+   - Load Image File (F)
+   - Initialize Convolutional kernel, image size (M,N), mask size (V), and thresholding
+   - Loop (x,y) With inc. 9
+   - Calculation of the mask with image segment in the loop with Convolution for (x,y) = 0 to V-1 during masking operation
+   - Thresholding
+   - Display Images
+   - End

+   - Start
+   - Load Image File (F)
+   - Initialize Convolutional kernel, image size (M,N), mask size (V), and thresholding
+   - Gaussian Smoothing
+   - Loop (m,n) With inc. 9
+   - Convolution of the image segment in the loop with 4th order Laplacian.
+   - Thresholding
+   - Display Images
+   - End

FIGURE 9.13 Algorithms for edge detection using (a) convolutional kernels, (b) compass edge detector, (c) the Canny operator.