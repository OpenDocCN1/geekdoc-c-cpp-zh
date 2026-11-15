This process is repeated for every interior pixel in the image. Pixels on the boundaries are missing one of the four adjacent pixels just described (corner pixels are missing two) and will not be modified in this application.

# 4. ALGORITHM DEVELOPMENT

We first develop the decomposition outline because it breaks the solution into a series of sequential steps.

# Decomposition Outline

+   (1) Read the header information.
+   (2) Write header information to the new file.
+   (3) Read the pixel values.
+   (4) Perform smoothing on each interior pixel.
+   (5) Write smoothed pixel values to the new file.

Steps 1 and 2 involve reading the header information from the data file and preserving this information by writing it to a new file. We will write a function to perform this task. Step 3 requires reading the pixel values into a two dimensional array. The array size depends on the information in the header, so we will use the vector class to define a two-dimensional array type pixel. Step 4 involves performing a smoothing modification on the image. We will write a second function to perform this task. To easily store and modify the pixel elements in the image, we will use the pixel class developed in Section 10.02. The refinement in pseudocode can now be developed:

# Refinement in Pseudocode

```
main():
    open data files
    read_header(fin, fout, width, height, max_color)
    read image
    smooth(image,width, height)
    write image
read_header(fin, fout, width, height, max_color):
    read magic_num
    while(next_ch == '#')
        read comment_line
        write comment_line to new file
    read width, height, max_color
    write width, height, max_color
smooth(image, width, height):
    set i to 0
    set j to 0
```