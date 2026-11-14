```
/* Convolve the input image with the kernel. */
for r = 0:1:(N-K)
    sum = 0;
    for i = 0:1:(K-1)
        for j = 0:1:(K-1)
            sum = sum + input_image(r+i1, c+j1) * kernel(i1,j1);
        end
    end
    output_image(r+dead_rows+1, c+dead_cols+1) = (sum1 / normal_factor);
end
end
```

# FIG. 3.3 MATLAB code for a 2D convolution of an input image with a kernel (matrix of coefficients).

```
Function [ image_buffer3 ] = combthreshold(image_buffer1, image_buffer2, T)
    N = Length(image_buffer1); % for now images are squares
    % pre-allocation and zeroing of the output image
    image_buffer3 = zeros(N); % for now images are squares
    image_buffer3(max(abs(image_buffer1), abs(image_buffer2))>T) = 255;
    % statement below is not needed when considering the pre-allocation and zeroing
    %image_buffer3(max(abs(image_buffer1), abs(image_buffer2))<T) = 0;
end
```

# FIG. 3.4 MATLAB code to assign black or white to each pixel of the output image based on the threshold T and to the individual pixels of two input images.

Other sections of the edge detection benchmark include (a) the merging of two images resulting from two convolutions & use different kernel values in a single image and (b) the generation of a B&W image (0 or 255 values) based on a threshold (T). Both computations are implemented in the combthreshold function shown in Fig. 3.4. The code for this function relies on MATLAB's ability to use matrices and to specify logical indexing. While this code result is very compact, it requires the use of temporary matrices to store intermediate results. The MATLAB statement max(abs(image_buffer1), abs(image_buffer2)) returns a matrix whose elements are the maximum values between the respective elements of abs(image_buffer1) and abs(image_buffer2). The result of max(abs(image_buffer1), abs(image_buffer2))>T provides a matrix of 1's and 0's indicating whether each element of the matrix max(abs(image_buffer1), abs(image_buffer2)) is larger than T or not.

Thus, in this example, four temporary matrices are used (including the two temporary matrices resultant from abs(image_buffer1) and abs(image_buffer2)). A translation pass from MATLAB to C would have to decide whether to use these temporary matrices, or instead decompose operations in a way that element-wise operations can be used, thus reducing memory use since the temporary matrices would not be needed. Fig. 3.5 presents another version of the combthreshold function, similar to the original C code, and Fig. 3.6 shows a MATLAB version obtained by a statement-by-statement translation from the original C code. These two versions make use of element-wise operations.