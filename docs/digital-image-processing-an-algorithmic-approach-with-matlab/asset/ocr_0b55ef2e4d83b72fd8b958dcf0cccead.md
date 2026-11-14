+   - The watermark is mapped with the significant coefficients of the transformed image and then inverse-transformed to retrieve the image representation.
+   - Modifications in a watermarked image, such as addition of noise, rotation, cropping, and compression, can increase the watermark distortion so much that it may not be recoverable.
+   - Robustness can be achieved in the watermarked images through redundant watermarks, multiple watermarks, and mapping the watermarks using transformed binary images rather than the image itself.
+   - This is still an open area of research, and newer techniques are discovered every now and then.

# 11.8 EXERCISES

+   1. In Figure 11.4, a noise attack has been simulated. Repeat the same exercise with rotation attack, that is, after embedding the watermark, rotate the whole image by 450° and then repeat the same operation with –450°. Then try to recover the watermark.
+   2. Repeat Q #1 for 10% cropping from all sides.
+   3. Repeat Q #1 for JPEG compression. In this case, save the image as a 70% compressed JPEG image, then reopen it and apply the procedure to recover the watermark.
+   4. Apply the methodology that resulted in Figure 11.3, but use the DWT instead of the DCT. Refer to Section 5.3 for details of the transformation. Embed the watermark with HH coefficients.
+   5. Repeat Q #4 but embed the watermark with HL, LH, and HH components in the top-left, top-right, and bottom-right corners, respectively. Refer to Section 5.3 for explanation of these terms.