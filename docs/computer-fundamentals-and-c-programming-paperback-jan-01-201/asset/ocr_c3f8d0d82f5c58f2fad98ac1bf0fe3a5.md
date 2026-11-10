+   11.4 Write a program that uses a function named `take_input` to let a user input an *unspecified* number of integers (not exceeding 100) before hitting EOF. The values should be stored in an array defined in `main` and the function is passed the name of this array as argument. How is this program superior to Program 11.5 in Chapter 11?
+   
+   11.5 Create a function named `print_array` that prints the contents of an array. The function must take an additional argument that determines whether the array is printed in forward or reverse sequence.
+   
+   11.6 Write a program that uses a function named `copy_array` to copy an initialized array.
+   
+   11.7 Write a program that uses a function named `copy_array2` to copy a 2D array that is defined and initialized in `main`.
+   
+   11.8 Write a program that uses a function named `day_diff` to compute the number of days between two days of *the same year* (both days inclusive). The days are input in the format DD:MM and don’t relate to a leap year.
+   
+   11.9 Devise a function named `time2download` that accepts the Internet speed in Mbps and file size in MB as two arguments. The function should return the download time in hours as a floating point number. (Note: Speed uses bits and file size uses bytes.)
+   
+   11.10 The volume of a cylinder is the product of the area of the base (PI * r * r) and the height. Write a program that accepts the radius and height from the user and invokes a function named `volume` which in turn invokes a function named `area`.
+   
+   11.11 Write a program that draws a rectangle using the `draw_rectangle` function. This function invokes the `draw_line` function for drawing the horizontal sides. Both functions need an additional argument that determines the character used for drawing.
+   
+   11.12 Write a program that uses recursive functions to (i) compute the sum of array elements, (ii) print the elements.
+   
+   11.13 Write a program that displays the Fibonacci numbers up to n terms using (i) a recursive function named `fibonacci_rec`, (ii) an iterative function named `fibonacci_it`. The value of n is set by user input. The program must track and print the total number of recursive calls and loop iterations made by the two functions. As you increase the value of n, *what observations can you make from the results?*