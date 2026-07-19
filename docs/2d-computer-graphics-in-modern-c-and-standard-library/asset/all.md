![](media/resources/title_page.png)

![2D Computer Graphics in Modern C++ and Standard Library](media/resources/title_page.png)

**2D Computer Graphics in Modern C++ and Standard Library**

Håkan Blomqvist

This book is for sale at [http://leanpub.com/2dcomputergraphicsinmoderncandstandardlibrary](http://leanpub.com/2dcomputergraphicsinmoderncandstandardlibrary)

This version was published on 2023-12-21

[![publisher's logo](media/resources/publisher-logo.png)](https://leanpub.com/)

*   *   *   *   *

This is a [Leanpub](https://leanpub.com) book. Leanpub empowers authors and publishers with the Lean Publishing process. [Lean Publishing](https://leanpub.com/manifesto) is the act of publishing an in-progress ebook using lightweight tools and many iterations to get reader feedback, pivot until you have the right book and build traction once you do.

*   *   *   *   *

© 2023 Håkan BlomqvistDedicated to all my friends around me. You know who you are.

## Guide

1.  [Cover](text/cover.xhtml)

![](resources/Introduction.jpg)

Figure 1

# 2D Drawing Basics

We have all been there when you want to present some data nicely and graphically. You start by implementing a GUI library so that you can set up a canvas to draw on… but then what? Or you can download and build a library that can handle reading and writing PNG images, as you need lossless images. Or you do the same to find out a file’s entropy. Or you’re coding on a game and want to test the look of animation sprites in a parallax setting. Whatever the reason is… it’s too complicated to do and takes longer than you would consider doing. So, no presentation, no collaboration, and no investigation using graphics.

It should just be easy to create graphics in standard C++. And this book is all about that. How do we draw a pixel, a line, or a circle? Those are questions we are going to answer.

## History

2D drawings with computers started in academia, as most things are computer-related. It was first created as a visualization tool for scientists and engineers in the US government and US corporate research centers such as Bell Labs and Boeing in the 1950s. Later, the tools would be developed at universities in the ’60s and ‘70s, such as Ohio State University, MIT, University of Utah, Cornell, North Carolina, and the New York Institute of Technology. The early breakthroughs in academic centers continued at research centers such as the famous Xerox PARC in the 1970s. These efforts broke into broadcast video graphics and major motion pictures in the late 70¹s and early 1980s. Computer graphic research continues today worldwide, now joined by entertainment and production companies’ research and development departments.

Since 1974, ACM SIGGRAPH has become an international community of researchers, artists, developers, filmmakers, scientists, and business professionals interested in computer graphics and interactive techniques. Each year, the latest and greatest of this research is presented.

## Standard Library

There needs to be more support for drawing in the Standard Library. There is no media support whatsoever in the Standard Library. And there is no need to. With the tools available to us, we will be able to draw pixels, lines, and circles.

## Compile Code Examples

All code is compiled using Clang++ but works fine with G++. Everything is C++20.

## Prerequisite

You’ll need to know how to program in C++ already. This book is about how to draw rather than how to program.

If you find the beginning to be too easy, then jump ahead to chapter **‘Advanced Examples’**

### Download the source code

![The source code is included in the extras, that is available here:](resources/sourcecode.jpg)

Figure 2\. The source code is included in the extras, that is available here:

Compile all examples using: `./build_and_run_all.sh`

* * *

# Draw Pixels with Standard Library

We’re using RGB elements to draw a pixel in C++. To handle RGB elements as one unit for convenience, there is something called `std::tuple.`

Reference: [https://en.cppreference.com/w/cpp/utility/tuple](https://en.cppreference.com/w/cpp/utility/tuple) e.g., a function that takes three integers as input and returns it as a tuple

`01_tuples.cpp` demonstrates the usage of `std::tuple` in `C++20.` It uses a tuple to store and manipulate RGB color elements as a single entity. The code includes the `<tuple>` and `<iostream>` headers and defines a function `get_rgb_elements_as_a_tuple` that takes three integers (`r,` `g,` and `b)` and returns a tuple containing these integers.

The `main` function initializes three sets of RGB values (`r1,` `g1,` `b1,` `r2,` `g2,` `b2,` and `r3,` `g3,` `b3).` Initially, only the first set (`r1,` `g1,` `b1)` is given values, while the other two sets are initialized to `0.`

The code then prints the initial RGB values of all three sets. Next, it calls `get_rgb_elements_as_a_tuple` with the first set of RGB values (`r1,` `g1,` `b1)` and assigns the returned tuple to `RGB.`

Two different methods are then used to `unroll` the tuple into the other two sets of RGB values:

1.  `unroll #1:` Using `std::get` to access individual elements of the tuple by index and assigning them to `r2,` `g2,` and `b2.`
2.  `unroll #2:` Using `std::tie` to unpack the tuple into `r3,` `g3,` and `b3.`

After each unroll, the RGB values of all three sets are printed to verify that the tuple has been correctly unpacked into the second and third sets of RGB values.

take a look in source_code.zip: `01_tuples.cpp`

Now, we know how to store and unroll a tuple of RGB elements. Let’s talk about adding rgb tuples to an image — to set a pixel where we want it to be in the image.

But before that, we need to discuss how computer memory (`1D)` is physically represented and the representation of an image (`2D).` To know where to store the tuple, we must translate (`2D)` into (`1D).` Store the pixel at a certain `x` and `y` in the `image,` but `in memory.`

`index = x + width * y`

![](resources/img_grid.jpg)

Figure 3

`X + width * Y = 2 + 10 * 3 = 32` `Index = 32`

Let’s create a function that handles the index calculations for us. A function that takes `X` and `Y` as input and returns the index.

Or, take a look in source_code.zip: `02_index.cpp`

Besides calculating the index, we need to know how many tuples we need to store in a `std::vector` for a defined `width` and `height` of an image. For instance, an image that has a width of `640` and a height of `360` is `640 * 360 (230400)` in size for a `std::vector` with those dimensions.

Reference: [https://en.cppreference.com/w/cpp/container/vector](https://en.cppreference.com/w/cpp/container/vector) As always, we need to include the header: `#include <vector>.`

To set the vector container size, we calculate it by multiplying the image width by the `height.` We use the `Resize function` in `std::vector` to set the size of the vector. Then we can use the vectors `operator[]` and `operator=` for index and assigns.

Also, why not assign black to all the pixels while we are at it as a clear image function?

For the source code, take a look in source_code.zip: `03_calcsize.cpp`

**Note** that this code example uses double for the RGB elements. The red, green, and blue are double numbers between `0.0` and `1.0,` not an integer between 0 - 255\. Enough with the calculations of the image metadata. It’s time to draw some pixels and save them into a text file. Yes, there are a few text-based image formats. We will use ``The PPM file format in this book. The graphics format comes from the open-source Netpbm project with several graphics programs and a programming library — used mainly in the Unix world. PPM stands for Portable PixMap format and is portable because it is written as ASCII (Type: P3`).`` A PPM file consists of two parts: a header and the image data. Don’t worry about it being ASCII; PPM can be converted to PNG, JPG, or any other format. Here’s what the PPM format looks like as ASCII:

```
 1 `P3    # "P3" means this is an RGB color image in ASCII.`
 2 `3 2   # "3 2" is the width and height of the image in pixels.`
 3 `255   # "255" is the maximum value for each color.`
 4 `# The part above is the header.`
 5 `# The part below is the image data: RGB triplets.`
 6 `255   0   0  # red`
 7 `  0 255   0  # green`
 8 `  0   0 255  # blue`
 9 `255 255   0  # yellow`
10 `255 255 255  # white`
11 `  0   0   0  # black`
```

Figure 4

The header starts with the `P3` indicator. The second line contains the width and height of the image, separated by whitespace. The third line has the number `255` stated; this will be used for all examples in this book. The `255` is the max value for each `rgb elements.` Below the header, each pixel is represented as three integer values between `0 - 255` for the RGB.

Include header: `#include <fstream>` Reference: [https://en.cppreference.com/w/cpp/io/basic_fstream](https://en.cppreference.com/w/cpp/io/basic_fstream)

For the source code, take a look in source_code.zip: `04_helloworld.cpp`

![04_helloworld_square.ppm](resources/04_helloworld_square.jpg)

Figure 5\. 04_helloworld_square.ppm

![04_helloworld.ppm](resources/04_helloworld.jpg)

Figure 6\. 04_helloworld.ppm

That’s great, but it would be even more awesome if we could read a PPM image.

For the source code, take a look in source_code.zip: `05_randomwalker.cpp`

![05_randomwalker.ppm](resources/05_randomwalker.jpg)

Figure 7\. 05_randomwalker.ppm

Now, we have a lot of code to go through in the `05 example.` One new header and a few new functions need some explanation.

`Example 05` was not only about reading a `PPM file.` We implemented a random walker. Let’s go through the code function by function.

Reference: [https://en.cppreference.com/w/cpp/header/random](https://en.cppreference.com/w/cpp/header/random)

Add random header to the file: `#include <random>`

The following functions are new:

*   `walker`
*   `update_x_and_y`
*   `read_image`
*   `get_color`
*   `get_width_and_height`
*   `startsWithCaseInsensitive`

We start by reading `04_helloworld.ppm` into image1 and, at the same time, set `width` and `height` from the PPM file using `get_width_and_height.` `read_image` uses the helper function `startsWithCaseInsensitive` to sort through the PPM data. `get_color` is used to read the RGB color.

We use the walker function to implement a random walker algorithm. Walker uses a random function to randomize the steps. We use the `update_x_and_y` function for each walker generation to move the walker in a random direction.

* * *

## Texture Generation with Standard Library

Neat, now we can draw pixels. Let’s play around with that a bit and generate different types of textures that can be useful.

Let’s generate textures using boolean `XOR` (`Exclusive-OR)` `AND` and `OR.`

The code generates and saves three textures based on bitwise operations: `XOR,` `AND,` and `OR.` It defines several functions to create, manipulate, and save the images to achieve this. The `get_index` function converts `2D` grid coordinates `(x, y)` into a `1D` array index, while the `calc_size` function calculates the total number of elements in a `2D` grid. The `clear_image` function sets all the pixels of an image to a given color, effectively clearing the image.

The code also provides three functions to create different textures: `draw_xor,` `draw_and,` and `draw_or.` Each function iterates through the image’s pixels and calculates the corresponding bitwise operation (`XOR,` `AND,` or `OR)` on the `x` and `y` coordinates of each `pixel.` The resulting value is then used as the color intensity for that pixel.

In the `main` function, the program starts by initializing the image vector and color tuple, then resizing the image vector based on the calculated size. The image is then cleared using a dark blue color. After that, the XOR texture is generated and saved to the `06_xor_texture.ppm` file. Subsequently, the AND texture is generated and saved to the `06_and_texture.ppm` file. Finally, the OR texture is generated and saved to the `06_or_texture.ppm` file.

For the source code, take a look in source_code.zip: `06_xor_and_or_texture.cpp`

![06_xor_texture.ppm](resources/06_xor_texture.jpg)

Figure 8\. 06_xor_texture.ppm

![06_and_texture.ppm](resources/06_and_texture.jpg)

Figure 9\. 06_and_texture.ppm

![06_or_texture.ppm](resources/06_or_texture.jpg)

Figure 10\. 06_or_texture.ppm

XOR, AND, and OR type of textures are the simplest ones. It’s just `x XOR y,` `x AND y,` or `x OR y.`

These textures are nice if you want to do an example. Excellent for prototyping use.

Procedural texture generation is another way to create textures. With random noise, we can generate textures like `clouds,` `marble,` and `wood.`

Reference: [https://en.cppreference.com/w/cpp/numeric/math/fabs](https://en.cppreference.com/w/cpp/numeric/math/fabs)

This code generates and saves three textures: Clouds, Marble, and Wood. It includes several functions to create, manipulate, and save images. The `get_index,` `calc_size,` `clear_image,` and `save_image` functions were explained in the previous response, and they serve the same purpose here. A new function, `generate noise,` is introduced, which fills a noise vector with random values in the `0.0` to `1.0` range.

This code’s core is the `smooth noise,` `turbulence,` and texture generation functions (`generate_cloud,` `generate_marble,` and `generate_wood).` The `smooth noise` function calculates a bilinear interpolation of the noise values at a given position. In contrast, the `turbulence` function sums up the smooth noise values at different scales to generate more complex patterns.

The `generate_cloud` function uses the `turbulence` function to create a cloud-like texture. In contrast, the `generate_marble` function calculates a sine pattern distorted by turbulence to mimic the appearance of marble. Finally, the `generate_wood` function creates a wood-like texture by calculating the distance from the center of the image and applying a sine pattern combined with turbulence.

In the `main` function, the program initializes the noise and image vectors and resizes them based on the calculated size. The image is then cleared using a dark blue color. The noise vector is generated, and the Cloud texture is created and saved to the `07_cloud_texture.ppm` file. Subsequently, the Marble texture is generated and saved to the `07_marble_texture.ppm` file. Finally, the Wood texture is generated and dedicated to the `07_wood_texture.ppm` file.

For the source code, take a look in source_code.zip: `07_clouds_marble_wood_texture.cpp`

![07_cloud_texture.ppm](resources/07_cloud_texture.jpg)

Figure 11\. 07_cloud_texture.ppm

![07_marble_texture.ppm](resources/07_marble_texture.jpg)

Figure 12\. 07_marble_texture.ppm

![07_wood_texture.ppm](resources/07_wood_texture.jpg)

Figure 13\. 07_wood_texture.ppm

It uses `bilinear interpolation` to smooth the noise. `Turbulence` is added for `marble` and `wood.`

* * *

## Time to draw some lines with Standard Library

Well, first, we go through some theory about light and color that is good to know.

A C++ program designed to manipulate images in the PPM format, specifically the P3 (ASCII) format. It includes various functions to perform image manipulation tasks such as creating a negative image, adjusting brightness and darkness, converting to grayscale, swapping color channels, and blending two images. The program uses the Standard Library and has a main function to perform user-specified manipulations on an input image file and save the result to an output file.

The code begins by importing necessary headers and declaring utility functions like `startsWithCaseInsensitive,` `get_index,` `calc_size,` `get_width_and_height,` and `get_color.` These functions help with string manipulation, getting an index in a 1D array representing a 2D image, calculating the size of an image, and extracting image dimensions and color values from strings.

The `read_image` function reads an image from a file and stores it as a vector of tuples with double values representing each pixel’s red, green, and blue (RGB) components. The function reads the file line by line, determining the file format, dimensions, and maximum color value, and then populates the image vector with the pixel data.

Several functions perform image manipulations like `negative_image,` `double_as_dark,` `onefive_as_dark,` `twice_as_bright,` `add_for_brighter,` `sub_for_darker,` `greyscale_image,` `zero_gb_image,` `r_zero_b_image,` `rg_zero_image,` `grb_image,` `bgr_image,` `rrb_image,` and `blended_two_images.` These functions take an image (vector of tuples) and its dimensions as input and modify the image. Some functions also take additional parameters like the blending factor `alpha` for `blended_two_images.`

The program’s `main` function reads an input image file, performs the user-specified image manipulations using the above-mentioned functions, and writes the modified image to an output file. The main function also validates the user input and ensures the provided parameters are valid.

For the source code, take a look in source_code.zip: `08_light_and_color.cpp`

For every image generated, `04_helloworld.ppm` gets reverted.

![08_negative_image.ppm](resources/08_negative_image.jpg)

Figure 14\. 08_negative_image.ppm

**Subtraction** Eg. original color `rgb(203, 37, 101)` as negative: `rgb(255-203, 255-37, 255-101)` which is the same as: `rgb(52, 218, 154).`

![08_double_as_dark.ppm](resources/08_double_as_dark.jpg)

Figure 15\. 08_double_as_dark.ppm

**Division** Eg. `rgb(203, 37, 101)` as double as dark: `rgb(203/2, 37/2, 101/2)` which is the same as: `rgb(101, 18, 50).`

![08_onefive_as_dark.ppm](resources/08_onefive_as_dark.jpg)

Figure 16\. 08_onefive_as_dark.ppm

**Division** Eg. `rgb(203, 37, 101)` as 1.5 as dark: `rgb(203/1.5, 37/1.5, 101/1.5)` which is the same as: `rgb(135, 25, 67).`

![08_twice_as_bright.ppm](resources/08_twice_as_bright.jpg)

Figure 17\. 08_twice_as_bright.ppm

**Multiplication** Eg. `rgb(203, 37, 101)` as twice as bright: `rgb(203x2, 37x2, 101x2)` which is the same as: `rgb(255, 74, 202).`

![08_add_for_brighter.ppm](resources/08_add_for_brighter.jpg)

Figure 18\. 08_add_for_brighter.ppm

**Addition** Eg. `RGB(203, 37, 101)` add for brighter: `RGB(203+30, 37+30, 101+30)` which is the same as: Eg. `RGB(233, 67, 131)`

![08_sub_for_darker.ppm](resources/08_sub_for_darker.jpg)

Figure 19\. 08_sub_for_darker.ppm

**Subtraction** Eg. `RGB(203, 37, 101)` sub for darker: `RGB(203-30, 37-30, 101-30)` which is the same as: Eg. `RGB(173, 7, 71)`

![08_greyscale_image.ppm](resources/08_greyscale_image.jpg)

Figure 20\. 08_greyscale_image.ppm

`Greyscale = (0.2126*R) + (0.7152*G) + (0.0722*B);`

![08_zero_gb_image.ppm](resources/08_zero_gb_image.jpg)

Figure 21\. 08_zero_gb_image.ppm

`R = 0;`

![08_r_zero_b_image.ppm](resources/08_r_zero_b_image.jpg)

Figure 22\. 08_r_zero_b_image.ppm

`G = 0;`

![08_rg_zero_image.ppm](resources/08_rg_zero_image.jpg)

Figure 23\. 08_rg_zero_image.ppm

`B = 0;`

![08_grb_image.ppm](resources/08_grb_image.jpg)

Figure 24\. 08_grb_image.ppm

`RGB => GRB`

![08_bgr_image.ppm](resources/08_bgr_image.jpg)

Figure 25\. 08_bgr_image.ppm

`RGB => BGR`

![08_rrb_image.ppm](resources/08_rrb_image.jpg)

Figure 26\. 08_rrb_image.ppm

`RGB => RRB`

![08_blended_two_images.ppm](resources/08_blended_two_images.jpg)

Figure 27\. 08_blended_two_images.ppm

Or blend two images as above (based on bg: `06_xor_texture.ppm` and fg: `04_helloworld_square.ppm).` Or as below, with bg: `05_randomwalker.ppm` and fg: `04_helloworld.ppm.`

![08_blended_two_images(2).ppm](resources/08_blended_two_images2.jpg)

Figure 28\. 08_blended_two_images(2).ppm

But now, let’s draw some lines.

This program is designed to generate two images: one with random lines and another with a damped sine wave. The program includes various utility functions, including line drawing, color conversion, line clipping, and saving images.

The `main` function initializes the image as a vector of tuples, each representing a pixel color in RGB values. It first generates random lines by picking random points and colors, then checks if the line is within the image’s dimensions using line clipping. The line is drawn on the image if it passes the clipping check. The resulting image, containing 15,000 random lines, is saved as `09_random_lines.ppm.`

Next, the program creates an image of a damped sine wave. The image is initialized with a clear background and a red line in the middle. The sine wave is drawn in black, and its damping factor is represented in grey. The damped sine wave image is saved as `09_damped_sine.ppm.`

To achieve these functionalities, the program utilizes functions like `get_index` and `calc_size` to handle image indexing and size calculations, `clear_image` to set the image background to white, and `h_to_rgb` to convert hue values to RGB. Additionally, the program uses `draw_line` to draw lines on the image, `find_region` and `clip_line` to handle line clipping, and `save_image` to save the generated images to a file in PPM format.

Bresenham’s line algorithm, used in the `draw_line` function, is an efficient and widely-used technique for drawing lines on a raster grid, such as a computer screen or a digital image. Developed by Jack E. Bresenham in 1962, the algorithm is notable for its simplicity, speed, and ability to produce accurate line drawings using only integer arithmetic. It works by plotting a series of points between two given endpoints, considering the discrete nature of raster grids and minimizing the error between the ideal line and the plotted points.

The algorithm begins by calculating the differences in the `x` and `y` coordinates of the two endpoints and then determining the absolute values of these differences to establish the overall slope of the line. Based on the slope, the algorithm chooses whether to increment the `x` or `y` coordinate at each step, depending on which produces the most minor error. It maintains an error variable accumulating the difference between the ideal line and the plotted points. This error variable decides when to increment the other coordinate to keep the line as close to the perfect line as possible.

Bresenham’s line algorithm is particularly well-suited for computer graphics because it avoids using floating-point arithmetic and division, which can be computationally expensive. Instead, it relies on integer operations, which are generally faster and more efficient. This makes the algorithm ideal for low-level graphics systems, such as early computer displays and video game consoles, where computational resources are limited.

The `find_region` and `clip_line` functions use the Cohen-Sutherland line clipping algorithm. This algorithm determines the parts of a line segment within a rectangular viewport or window. The main goal of the algorithm is to reduce the amount of line drawing computation required for lines that are partially or entirely outside the viewport.

The Cohen-Sutherland algorithm assigns a 4-bit region code to each line segment endpoint based on its position relative to the viewport. The bits correspond to the top, bottom, right, and left regions outside the viewport. The `find_region` function computes this region code for a given point. If both endpoints have a region code of 0, the line segment is entirely inside the viewport, and no clipping is required. If the bitwise AND of the two region codes is non-zero, the line segment is altogether outside the viewport and can be discarded.

When a line segment straddles the viewport boundary, the `clip_line` function comes into play. This function iteratively clips the line segment against each viewport edge by calculating the intersection point between the line and the border. It then replaces the endpoint outside the viewport with the intersection point and updates its region code. This process is repeated until the line segment is either entirely inside the viewport or determined to be outside the viewport.

For the source code, take a look in source_code.zip: `09_lines.cpp`

![09_random_lines.ppm](resources/09_random_lines.jpg)

Figure 29\. 09_random_lines.ppm

In this example, we use `HSV` (`Hue,` `Saturation,` and `Value)` as a color model and convert it back to `RGB` afterwords. A random `Hue` gets produced, and with the `h_to_rgb(float h)` function, we get a `RGB` value back.

We also use the `clip_line` function and `find_region` function for clipping every line between the visible and non-visible screen.

`std::mt19937` is a C++ standard library implementation of the Mersenne Twister pseudorandom number generator (PRNG) algorithm. The name “mt19937” is derived from the Mersenne Twister using a Mersenne prime number, 2^19937 - 1, as the basis for its internal state. This PRNG is widely used for its high-quality random number generation, significant period, and efficient performance. Mersenne Twister is a popular choice for various applications, including simulations, statistical modeling, and computer games, where high-quality random numbers are needed.

The `std::mt19937` generator is part of the C++11 `<random>` header or newer, which provides a comprehensive suite of random number generation facilities. This header includes the Mersenne Twister and other random number generators, probability distributions, and other utility functions for generating random numbers. The `<random>` library is designed to offer a more versatile and flexible approach to random number generation compared to older C++ functions like `rand()` and `srand().`

To use `std::mt19937,` you first need to create an instance of the generator and seed it with an initial value. The quality of the random numbers generated depends on the seed value, typically derived from a high-resolution clock or other sources of entropy. Once the generator is seeded, you can use it to generate random numbers within a specified range or to generate random numbers according to a probability distribution using distribution classes provided by the ``` header.

![09_damped_sine.ppm](resources/09_damped_sine.jpg)

Figure 30\. 09_damped_sine.ppm

Here, we use the previous `X` and `Y` to draw a continuous line shaped into the damped sine as calculated.

A damped sine wave is a sinusoidal function that gradually decreases in amplitude over time due to the presence of a damping factor. In mathematical terms, a damped sine wave can be represented as `A(t) = A₀ * sin(ωt + φ) * e^(-αt),` where `A₀` is the initial amplitude, `ω` is the angular frequency, `φ` is the phase, `α` is the damping factor, and `t` represents time. The damping factor, `α,` determines the rate at which the amplitude decreases; a more significant damping factor results in a more rapid decrease in amplitude, while a smaller damping factor causes the amplitude to decay more slowly.

Damped sine waves can be effectively used in animations to create natural-looking motion or simulate physical processes involving oscillatory behavior. For example, they can animate a pendulum’s movement, the ball’s bouncing, or the spring’s oscillation. In these cases, the damped sine wave helps model the gradual energy loss due to friction, air resistance, or other dissipative forces in real-world systems. By incorporating damped sine waves into animations, designers can create more realistic and visually appealing motion that closely mimics the behavior observed in nature, making the animation more immersive and engaging for the audience.

Also, we can draw a line with starting `x` and `y` points, length, and degrees.

![09_angle_lines.ppm](resources/09_angle_lines.jpg)

Figure 31\. 09_angle_lines.ppm

The code is designed to create an image with lines drawn at different angles. The code begins with several include statements, bringing in necessary libraries and a series of function definitions.

The `get_index,` `calc_size,` and `clear_image` functions are utility functions for image manipulation. `get_index` calculates a one-dimensional index from two-dimensional coordinates, `calc_size` calculates the total size of the image given its width and height, and `clear_image` sets all pixels in the image to white.

`draw_line` is a function that draws a line between two points in the image with a specified color. The `find_region,` `clip_line,` and `get_angle_line` functions are used for line clipping and angle calculations. `find_region` determines which region of the image a point lies in, `clip_line` clips a line to the image boundaries, and `get_angle_line` calculates the endpoint of a line given a starting point, angle, and length.

Finally, `save_image` is a function that writes the image data to a file in PPM format.

The `main` function initializes the image and sets its dimensions. It then draws lines at various angles `(0, 45, 90, 135, 180, 225, 270, and 315 degrees)` around the center of the image with a fixed length. The `clip_line` function ensures that lines are only drawn within the boundaries of the image. After drawing all the lines, the image is saved to a file named `09_angle_lines.ppm.`

* * *

## There are no straight curves, only curved lines

Bézier curve is a parametric curve. There are three types of Bézier curves:

*   Linear Bézier curves
*   Quadratic Bézier curves
*   Cubic Bézier curves

Linear Interpolation is a mathematical function that returns a value between two others at a point on a linear scale. Most commonly, it’s used for moving or changing values over a period of time. With the `std::lerp` (Linear Interpolation) function in C++20, we can draw curves using Linear, Quadratic, and Cubic Bézier curves (utilizing a `std::lerp` inception As they build on each other).

Reference: [https://en.cppreference.com/w/cpp/numeric/lerp](https://en.cppreference.com/w/cpp/numeric/lerp)

C++17 version: [https://github.com/emsr/cxx_linear](https://github.com/emsr/cxx_linear)

Use the Lerp and midpoint code above if you can only use C++17.

The C++ code demonstrates how to draw linear, quadratic, and cubic Bezier curves using dots on an image. It creates an image with various Bezier curves and saves the result as a PPM file. The code starts by including the necessary header files. Then, it defines several functions to compute the points on the Bezier curves, manipulate the image, and render the curves on the image.

The linear, quadratic, and cubic Bezier curve functions take the coordinates of the start, control, and endpoints, along with the number of splits as input, and compute the points on the curves. Utility functions are defined to help with image manipulation and rendering, such as getting an index in the image vector, calculating the size of the image, clearing the image, and drawing lines.

In addition to the Bezier curve functions, the code also has functions to draw the Bezier curve points and markers on the image, which are used for better visualization. Another function, `save_image,` is defined to save the image as a PPM file.

In the `main` function, the program initializes the `width` and `height` of the image, creates a vector for storing the image data, and clears the image. Next, it draws linear, quadratic, and cubic Bezier curves using previously defined functions. The program also draws the control lines and markers for better visualization. Finally, it saves the resulting image as a PPM file named `10_curved_dots.ppm.`

For the source code, take a look in source_code.zip: `10_curved_dots.cpp`

![10_curved_dots.ppm](resources/10_curved_dots.jpg)

Figure 32\. 10_curved_dots.ppm

This is what `std::lerp` does… these points can then use a `line` function and draw the curve. The curve is controlled with the two control points.

This C++ code is designed to create an image of curved lines using linear, quadratic, and cubic Bezier curves. It includes the necessary libraries and then defines several functions to calculate Bezier curves, draw lines and dots, and save the image.

The `linear_bezier_curves,` `quadratic_bezier_curves,` and `cubic_bezier_curves` functions are used to generate the points for linear, quadratic, and cubic Bezier curves, respectively. The `draw_line` function draws a straight line between two points. The `draw_xy_line` function draws a line using the points generated from Bezier curves, while the `draw_xy_dots` function draws dots at the points generated by the Bezier curves.

The `draw_marker` function creates a small marker at a specified point, and the `save_image` function saves the image to a file in PPM format.

In the `main` function, the code sets up an image of a specified width and height and fills it with a white background. Then, it draws lines using the Bezier curves functions, along with markers and dots at various points. Finally, it saves the created image to a file.

The code demonstrates the use of `linear,` `quadratic,` and `cubic Bezier` curves to create smooth curves between points in an image and draw markers and dots at specific points along the curve.

For the source code, take a look in source_code.zip: `10_curved_lines.cpp`

![10_curved_lines.ppm](resources/10_curved_lines.jpg)

Figure 33\. 10_curved_lines.ppm

Here, the curves are drawn with the `line` function, and the points and control points are marked.

* * *

## Rectangles with Standard Library

A rectangle is a closed 2D shape, having four sides, four corners, and four right angles (90°). The opposite sides of a rectangle are equal and parallel. Since a rectangle is a 2D shape, it is characterized by two dimensions: width and height. You’ll need `X` and `Y` together with the rectangles `width` and `height` to draw a rectangle.

The C++ code generates an image containing two rectangles, one outlined and one filled, saved as a PPM file. The code consists of several functions, each serving a specific purpose: to create and manipulate the image.

The first few functions in the code are used for primary image handling. The `get_index` function calculates the index of a pixel in a 1D vector representation of a 2D image given its (x, y) coordinates and the image width. The `calc_size` function calculates the size of the vision given its width and height, while the `clear_image` function fills the image vector with white pixels (R=1.0, G=1.0, B=1.0).

Next, there are functions for drawing shapes on the image. The `draw_line` function draws a line between two points in the image using Bresenham’s line algorithm, an efficient method for drawing lines on a raster grid. The `draw_rect` function draws an outlined rectangle by connecting its four corners using the `draw_line` function. On the other hand, the `draw_filled_rect` function draws a filled rectangle by iterating over its area and setting the color of each pixel inside the rectangle.

Finally, the `save_image` function saves the image to a PPM file, a simple, uncompressed image file format.

In the `main` function, the image parameters, such as width, height, and the position and size of the two rectangles, are initialized. Then, a vector representing the image is created and initialized with white pixels. After that, the two rectangles are drawn on the image. The resulting image is then saved to a PPM file named `11_rectangles.ppm.`

For the source code, take a look in source_code.zip: `11_rectangles.cpp`

![11_rectangles.ppm](resources/11_rectangles.jpg)

Figure 34\. 11_rectangles.ppm

Here, we have a rectangle and a filled rectangle.

The code reads a series of rectangle specifications from a file and then generates an image containing those rectangles, with a background color and overlapping filled rectangles. The primary purpose of the code is to create an image where the filled rectangles are blended with the background color using an alpha channel for transparency.

The code starts by including necessary headers and defining helper functions such as `startsWithCaseInsensitive,` `get_index,` `calc_size,` `clear_image,` `parse_bginfo_line,` `parse_rect_line,` `blend_colors,` `draw_filled_rect,` and `save_image.` These functions perform various operations, such as string manipulation, parsing input lines, calculating indices for a 2D image stored as a 1D vector, blending colors, drawing rectangles, and saving the final image as a PPM file.

In the `main` function, the program reads lines from the input file `11_squint_with_your_eyes.txt.` If a line starts with `r,` it is considered a rectangle specification and parsed using the `parse_rect_line` function. The rectangle’s `coordinates,` `color,` and `alpha` values are then used to draw the rectangle on the image using the `draw_filled_rect` function. If a line starts with `b,` it is considered a background specification and parsed using the `parse_bginfo_line` function. The `background color` and `image dimensions` are extracted from the line, and the image vector is resized accordingly. The `clear_image` function fills the entire image with the background color.

After processing all the lines from the input file, the program saves the resulting image to a PPM file called `11_squint_with_your_eyes.ppm` using the `save_image` function. The PPM file format is simple and text-based and stores pixel-color information as plain text. The code writes the PPM header, followed by the pixel color values, one pixel per line, in the output file.

For the source code, take a look in source_code.zip: `11_rectangles_from_file.cpp`

For the source code, take a look in source_code.zip: `11_squint_with_your_eyes.txt`

![11_squint_with_your_eyes.ppm](resources/11_squint_with_your_eyes.jpg)

Figure 35\. 11_squint_with_your_eyes.ppm

This is an example of how you can read data and present it in an image.

* * *

## Circles with Standard Library

A circle is a round-shaped figure that has no corners or edges.

The midpoint circle algorithm is widely used for efficiently drawing circles on raster displays, such as computer screens or images. The algorithm was developed as an extension of Bresenham’s line algorithm for drawing lines. The midpoint circle algorithm employs integer arithmetic and incremental calculations to minimize computational overhead and avoid using computationally expensive floating-point arithmetic, such as square root operations. It generates a set of points on the circle’s circumference, taking advantage of its inherent symmetry to reduce the required calculations.

The algorithm works by starting at the topmost point of the circle and incrementally moving towards the x-axis while calculating the appropriate y-coordinate for each x-coordinate. It does this by evaluating a decision parameter at each step to determine whether to increment the x-coordinate, the y-coordinate, or both. The decision parameter is based on the circle equation, and it helps to determine whether the midpoint between two candidate pixels is inside or outside the circle. If the midpoint is inside the circle, the algorithm chooses the pixel closer to the x-axis; if it is outside, the algorithm selects the pixel closer to the y-axis.

One of the key features of the midpoint circle algorithm is its ability to exploit the eightfold symmetry of a circle. Since a circle is symmetrical about both the x and y axes and the lines y = x and y = -x, the algorithm only needs to compute the points in one-eighth of the circle and then derive the remaining points by reflection. This significantly reduces the number of calculations required to draw the entire circle. The result is an efficient method for drawing circles in computer graphics, mainly when working with low-level raster graphics operations or limited computational resources.

This C++ code generates an image containing two circles, one filled and one unfilled, with a white background. The primary purpose of the code is to demonstrate the process of drawing circles using a simple implementation of the midpoint circle algorithm and saving the resulting image as a PPM file.

The code starts by including necessary headers and defining helper functions, such as `get_index,` `calc_size,` `clear_image,` `draw_circle,` `draw_filled_circle,` and `save_image.` These functions perform various operations, such as calculating indices for a 2D image stored as a 1D vector, clearing the image by setting all pixel colors to white, drawing unfilled and filled circles using the midpoint circle algorithm, and saving the final image as a PPM file.

In the `main` function, the program sets the width and height of the image, as well as the positions and radii of the two circles. The x and y coordinates, as well as the radius of the circles, are calculated based on the dimensions of the image. The image vector is resized accordingly, and the `clear_image` function is called to fill the entire image with the white background color.

Next, the `draw_circle` function is called to draw the first circle (unfilled) on the image, and the `draw_filled_circle` function is called to draw the second circle (filled) on the image. Both functions use the midpoint circle algorithm to determine which pixels to set to the desired color (black). The `draw_filled_circle` function fills the circle’s interior by drawing horizontal lines between the boundary points.

Finally, the `save_image` function is called to save the resulting image as a PPM file called “12_circle.ppm”. The PPM file format is simple and text-based and stores pixel-color information as plain text. The code writes the PPM header, followed by the pixel color values, one pixel per line, in the output file.

For the source code, take a look in source_code.zip: `12_circle.cpp`

![12_circle.ppm](resources/12_circle.jpg)

Figure 36\. 12_circle.ppm

Here, we have a circle and a filled circle.

A program that reads circle specifications from a text file and generates a Portable Pixmap (PPM) file containing an image of the circles. The code includes necessary libraries for file streams, tuples, vectors, and mathematical functions. Then, several utility functions are defined to perform tasks like case-insensitive string matching, index calculations, image size determination, and image clearing.

The program then includes functions for parsing the circle and background information from the input file. These functions, `parse_circle_line` and `parse_bginfo_line,` process each input file line and extract the relevant information. For circle specifications, it extracts the coordinates, radius, and color information; for background information, it extracts the image dimensions and color.

Next, the code defines several functions for color blending, region finding, and line clipping. The `blend_colors` function combines two colors based on their transparency, while `find_region` and `clip_line` determine which portions of the circle are visible within the image boundaries.

The program’s main functionality is found in the `draw_filled_circle` function, which takes the circle’s center coordinates, radius, color, and image dimensions as arguments. It uses an efficient algorithm to draw filled circles, updating the image buffer with the circle’s color. The `save_image` function saves the generated image to a PPM file.

Finally, the `main` function reads the input file and calls the appropriate functions to parse the circle and background information. It initializes an empty image and fills it with the background color, then iterates through each circle specification and draws the circle onto the image. Once all circles have been drawn, it saves the image to a file and exits.

For the source code, take a look in source_code.zip: `12_circles_from_file.cpp`

For the source code, take a look in source_code.zip: `12_squint_with_your_eyes.txt`

![12_squint_with_your_eyes.ppm](resources/12_squint_with_your_eyes.jpg)

Figure 37\. 12_squint_with_your_eyes.ppm

Another example is reading data and rendering an image.

Let`s draw a wedge using an arc.

The program’s wedge drawing algorithm combines trigonometry and Bresenham’s line algorithm. The trigonometric aspect calculates the points along the arc of the wedge, while Bresenham`s line algorithm is used to draw the straight lines that form the sides of the wedge.

To calculate the points along the arc, the algorithm begins by converting the starting and ending angles to radians. Then, it iteratively computes the x and y coordinates using the cosine and sine functions of the current angle and adds them to a list of coordinates. The iteration continues with a small increment in the angle until the ending angle is reached.

For the straight sides of the wedge, Bresenham’s line algorithm is used to connect the center of the circle to the start and end points of the arc. Bresenham’s line algorithm is a widely used technique for drawing lines in computer graphics, as it efficiently calculates the integer points along the line without using floating-point arithmetic. The algorithm iteratively updates the x and y coordinates while minimizing the error between the actual line and the drawn points. Combining the arc points and the lines generated by Bresenham`s algorithm creates the complete wedge shape.

![12_wedge.ppm](resources/12_wedge.jpg)

Figure 38\. 12_wedge.ppm

This C++ program generates an image with a radial pattern resembling a wedge or a pie slice. The image is saved in the PPM format.

The program begins by including necessary headers and defining functions for handling image data, such as calculating the size of the image, clearing it, and saving it to a file. It also contains functions to draw lines and filled and unfilled wedges on the image. The main part of the program initializes the image dimensions and creates an empty white image of the specified size.

The program then sets the center, radius, and angles for the wedge to be drawn. The center of the wedge is set to be the midpoint of the image, and the radius is set to 80% of half of the image height. The starting and ending angles of the wedge are defined in degrees, with 0 and 348 degrees being used in this example.

Next, the program draws a filled black wedge with the specified dimensions, followed by a filled gray wedge with half the radius, creating a “doughnut” shape. Then, it draws an unfilled purple wedge outline around the more prominent black wedge. Finally, the image is saved to a file named `12_wedge.ppm.`

For the source code, take a look in source_code.zip: `12_wedge.cpp`

* * *

## Triangles with Standard Library

A triangle is a closed, two-dimensional shape with three sides, three angles, and three vertices. A triangle is also a polygon.

Create an image containing two triangles, one outlined and the other filled, and save it as a PPM file. The code is divided into several sections, such as defining functions for operations on images, drawing lines and triangles, and the main program logic.

The program begins by including necessary headers and then defining several utility functions. The `get_index` function calculates the index of a given pixel in a 1D vector based on its x and y coordinates and the image width. The `calc_size` function calculates an image’s total number of pixels, given its width and height. The `clear_image` function sets all pixels in an image to a specified color.

The `draw_line` function uses a modified Bresenham’s line algorithm to draw a line between two points on an image. The `draw_triangle` and `draw_filled_triangle` functions utilize the `draw_line` function to draw the edges of triangles, either outlined or filled, using an incremental scanline rendering approach.

The `save_image` function takes an image represented as a vector of RGB color tuples, its width and height, and a filename as arguments and saves the image as a PPM file.

In the main function, the program first initializes the width and height of the image, as well as the coordinates of the vertices of the two triangles. It then creates a vector to store the image and sets its initial color to white using the `clear_image` function. Next, it sets the color to black and calls the `draw_triangle` function to draw the first triangle and the `draw_filled_triangle` function to draw the second triangle.

Finally, the program saves the image using the `save_image` function, resulting in a PPM file containing the two triangles.

For the source code, take a look in source_code.zip: `13_triangles.cpp`

![13_triangles.ppm](resources/13_trangles.jpg)

Figure 39\. 13_triangles.ppm

Here we have a triangle and a filled triangled

This C++ code reads a file containing information about triangles and their colors and then generates a raster image of the triangles. The program includes necessary headers like iostream, fstream, tuple, vector, random, cmath, and algorithm. It defines several utility functions to handle string processing, coordinate calculations, and image manipulation. The main part of the code consists of functions to parse input strings, blend colors, find the region of a point, clip lines, draw filled triangles, and save the generated image to a file.

The `parse_bginfo_line()` and `parse_triangle_line()` functions read lines from the input file and convert the data into the appropriate data types for further processing. The `blend_colors()` function is used to blend colors using the alpha value, which determines how transparent the color should be when applied to the image. The `find_region()` and `clip_line()` functions are used to determine if a point is within the image bounds and to clip any lines outside the image bounds.

The `draw_filled_triangle()` function renders triangles onto the image. It uses a scanline algorithm to fill the triangles with the specified color. This function handles edge cases and ensures the triangles are drawn correctly within the image boundaries. Finally, the `save_image()` function writes the generated image data to a file in PPM (Portable Pixmap) format.

For the source code, take a look in source_code.zip: `13_triangles_from_file.cpp`

For the source code, take a look in source_code.zip: `13_squint_with_your_eyes.txt`

![13_squint_with_your_eyes.ppm](resources/13_squint_with_your_eyes.jpg)

Figure 40\. 13_squint_with_your_eyes.ppm

Another example.

* * *

# Animation with Standard Library

Below are four examples of animation you can do… of course, the animation might be more related to graphs than images.

You can animate shapes, color transition, opacity, and movement.

A C++ program that creates a simple animation using a random walker algorithm. It reads an image file in PPM format, generates a sequence of images, and saves them in a specified directory. The user can then use a tool like FFmpeg to convert the image sequence into a video format.

The program begins by defining several helper functions for tasks such as reading and writing PPM images, updating the positions of the walkers, and blending two images. The ‘main’ function reads an image from a file, creates a second image buffer, and then initializes the walker positions to the center of the image. It then iterates over a loop for many steps, moving the walkers randomly in one of the four cardinal directions and updating the image buffer with the color from the first image at the new walker positions.

After every 100 steps, the program saves the current state of the image buffer as a new PPM file. The animation created by this program consists of two walkers moving randomly over the image, revealing its contents as they traverse it.

For the source code, take a look in source_code.zip: `14_animation05.cpp`

An animation program that generates a series of images based on input data from a text file. The text file contains information about the background and rectangles to be drawn on the images. The program begins by including necessary libraries and defining functions that will be used later. Functions include ‘startsWithCaseInsensitive’ for checking if a string starts with a specific substring, ‘get_index’ and ‘calc_size’ for converting 2D coordinates into 1D indices, and ‘clear_image’ for initializing an image with a specified background color.

The program also contains functions for parsing the input text file, such as ‘parse_bginfo_line’ and ‘parse_rect_line,’ which extract relevant information from the input lines. Another essential function is ‘blend_colors,’ which combines two colors based on their alpha values. The ‘draw_filled_rect’ function is responsible for drawing filled rectangles on the image using the ‘blend_colors’ function. The ‘get_filname’ function generates a filename for the output image, and the ‘save_image’ function saves the image to a file.

The ‘main’ function of the program begins by creating an output directory and opening the input text file. The program then iterates through each text file line, checking if the line starts with ‘r’ for the rectangle or ‘b’ for the background. If it begins with ‘r,’ the program parses the rectangle information, draws the rectangle on the image, and saves it. If the line starts with ‘b,’ the program parses the background information, resizes the image, sets the background color, and keeps the image. The program prints the filenames of the saved images to the console and closes the input file at the end.

For the source code, take a look in source_code.zip: `14_animation11.cpp`

It works the same as `14_animation11.cpp.` Uses circles instead of rectangles.

For the source code, take a look in source_code.zip: `14_animation12.cpp`

It works the same as `14_animation11.cpp.` Uses triangles instead of rectangles.

For the source code, take a look in source_code.zip: `14_animation13.cpp`

Just experiment and use what you think looks good.

* * *

# Drawing Charts and a Font

The flood-fill algorithm is a popular computer graphics and image processing technique for filling an area with a specified color. This algorithm works by starting at a seed pixel and recursively or iteratively filling neighboring pixels that share the same color as the seed pixel, ultimately replacing them with a new target color. The process continues until all the connected pixels sharing the original color are filled with the new color. The flood-fill algorithm has several variations, such as 4-way and 8-way connectivity, which determine how pixels are considered neighbors based on their relative positions.

Flood-fill algorithms have various applications, particularly in image editing software, computer games, and pattern recognition tasks. In image editing software, the flood-fill tool, commonly known as the paint bucket, fills areas with a uniform color or pattern. This tool allows users to easily modify images by changing the color of specific regions or creating new shapes. The flood-fill algorithm can be employed in computer games for tasks like procedural map generation, pathfinding, or detecting connected components in a game world. Flood-fill algorithms can identify and isolate distinct regions or objects within an image based on color or texture properties in pattern recognition.

Despite its popularity and numerous applications, the flood-fill algorithm does have some limitations. Its performance can be affected by the size of the area to be filled and the complexity of the image. Recursive implementations of the flood-fill algorithm are prone to stack overflows when dealing with large areas, while iterative implementations can be memory-intensive. Additionally, the algorithm may fail to provide the desired output if there are gaps or holes in the region’s boundaries to be filled. In such cases, modifications to the algorithm, like tolerance-based flood-fill techniques, can be applied to address these issues and achieve more accurate results.

A program that demonstrates the creation and manipulation of a radar chart, a graphical representation of multivariate data in the form of a two-dimensional graph. This code can be compiled using the command provided at the beginning of the code.

The program begins by including the required header files and defining functions to manipulate images, such as calculating the index, clearing the image, drawing shapes, and clipping lines. Some functions, like `get_index` and `calc_size,` are utility functions that help with image manipulation, while others, like `draw_circle` and `draw_filled_circle,` are responsible for drawing specific shapes on the image.

The `floodfill_algorithm` function implements the flood-fill algorithm that fills an enclosed area of an image with a specified color. The `get_all_ys` and `draw_line_coords` functions are used for drawing polygons on the image. The `draw_polygon` and `draw_filled_polygon` functions use these helper functions to draw and fill polygons.

The `draw_line` function takes an image, a set of coordinates, a color, and the width and height of the image and draws a line on the image using the given coordinates and color. The `find_region` and `clip_line` functions are used to clip lines based on the width and height of the image, ensuring that lines do not extend beyond the boundaries of the image.

For the source code, take a look in source_code.zip: `15_radarchart.cpp`

![15_radarchart.ppm](resources/15_radarchart.jpg)

Figure 41\. 15_radarchart.ppm

As the `15_radarchart.ppm` width is `1920` pixels and the height is `1080,` the size of the PPM is getting a bit big to write as a text file. The save_image()-function saves the PPM as a P6 with the RGB as 3-byte binary data.

This code is written in C++ and is used to generate a radial chart with three colored segments representing three different categories of data. The chart consists of 52 wedges, each representing a week. The data for each category is provided in three arrays: `a1,` `a2,` and `a3.` The chart is then saved as an image in PPM (Portable Pixmap) format.

The program begins by including the necessary header files and defining some utility functions for working with images, such as `get_index,` `calc_size,` `clear_image,` and others. These functions create and manipulate the image data structure, a vector of tuples representing RGB colors. Functions like `draw_filled_circle,` `draw_filled_wedge,` and `save_image` are used to draw and save the final image.

The `main` function starts by initializing the image data structure and setting up color tuples for the background and three data categories. It calculates the center of the image, the radius, and other necessary parameters for drawing the radial chart. It then draws a filled circle with a specific background color and iterates through the 52 wedges, drawing filled wedges for each of the three categories using the data provided in `a1,` `a2,` and `a3.` The wedges are drawn using the `draw_filled_wedge` function, which uses the `draw_line_coords` function to create line coordinates for the wedges. After drawing all the wedges, the image is saved to a file named “15_weekchart.ppm” using the `save_image` function.

For the source code, take a look in source_code.zip: `15_weekchart.cpp`

![15_weekchart.ppm](resources/15_weekchart.jpg)

Figure 42\. 15_weekchart.ppm

Also, as a `P6 PPM,` it has the same width and height as `15_radarchart.ppm.`

This C++ code reads and writes `P6 PPM` (`Portable PixMap)` image files. The main purpose is to load an image file and then save it to another file without any modification. The code is organized into three main sections: the `load_image` function, the `save_image` function, and the `main` function.

The `load_image` function refers to a vector of tuples of floats, width and height integers, and a string for the filename. It opens the file in binary mode, reads the magic number (which should be “P6”), skips any comments, reads the image dimensions and maximum color value, and then reads the pixel data into the vector of tuples. The pixel data is normalized by dividing the individual color values by `255.0,` which makes it easier to work with in future operations.

The `save_image` function returns an image to a file. It takes the same arguments as the `load_image` function, but instead of reading the data, it writes the image data to a file. It writes the magic number, image dimensions, maximum color value, and pixel data, converting the normalized float values to the `0-255` range.

The `main` function starts by defining a vector of tuples to store the image data and integer variables for width and height. It then calls the `load_image` function to read the image file, prints out the width and height of the image, and finally calls the `save_image` function to save the image data to a new file.

This code can be a starting point for more complex image manipulation tasks, as it provides a simple way to read and write PPM files.

To read a P6 PPM, take a look in source_code.zip: `15_read_p6_ppm.cpp`

Let’s create a font and render all the letters in it.

![](resources/screenshot-montage-font.jpg)

Figure 43

This code generates images of hand-drawn-styled letters and numbers. The program defines a set of functions to draw each character, using the Bresenhams line algorithm to get the points of the lines that make up the characters. It also defines functions to draw filled circles, clear the image, and save it in the `PPM` (Portable Pixmap) format.

The main function `draw_and_save_font` iterates through each character, draws it with the specified `color,` `width,` `height,` `margin,` and `line` size, and saves the resulting image to a `PPM` file.

Each `draw_font_<character>` function has two main components:

*   An array of points that define the character’s shape, where the points are represented by their relative X and Y coordinates.
*   An array of line segments that connect these points, where each line segment is represented by a pair of indices corresponding to the points array.

In each function, the code iterates through the line segments, calculates the coordinates of the actual points on the image canvas by scaling and translating the relative coordinates, and adds the points to the points vector.

The draw function takes the points vector and the other parameters and updates the image by drawing a single pixel (when the line size is 1) or drawing a filled circle centered at each point.

Finally, the save_image function writes the image data to a PPM file using the specified filename.

Here’s a brief explanation of the purpose of each function:

*   `draw_font_<character>:` Draws the specified character by adding line points to the points vector.
*   `get_line_points:` Uses the Bresenhams line algorithm to get the points of a line segment.
*   `draw_filled_circle:` Draws a filled circle centered at the specified point with the specified radius.
*   `clear_image:` Resets the image to a white background.
*   `save_image:` Saves the image to a PPM file with the specified filename.
*   `draw:` Updates the image with the specified points, color, line size, etc.
*   `draw_and_save_font:` Main function that iterates through each character, draws it and saves the image to a file.

To draw each letter in the font, look in source_code.zip: `15_draw_font.cpp`

* * *

![](resources/Middle.jpg)

Figure 44

# Presentation, Collaboration, and Investigation

## Presentation

Creating charts and diagrams can be a great way to visualize data and communicate information. This chapter will show you how to create 2D charts and graphs using C++.

We’ll start by showing you how to create basic shapes and lines. Then, we’ll make more complex shapes like circles and rectangles. Finally, we`ll show you how to add text and labels to your charts and diagrams.

By the end of this chapter, you’ll know how to create professional-looking 2D charts and diagrams using C++. So let`s get started!

## Draw a bar chart

Draw a bar chart by just hacking away.

This generates an image of a bar chart with specific characteristics. The chart has 5 bars and four icons drawn in the image and percentage values. The code is structured in various functions called the `main` function to build and save the image.

The program starts with the necessary includes, such as iostream, fstream, tuple, vector, random, and cmath. The `get_index` function calculates an index for accessing elements of the image vector. The `calc_size` function calculates the image size based on the width, height, and margin. The `clear_image` function initializes the image with a specific color (gray).

The `draw_filled_rect` function takes the position (x, y), dimensions (w, h), image reference, color, width, and height as parameters and draws a filled rectangle on the image. The `draw_line` function takes the image reference, a tuple of coordinates, color, width, and height as parameters, and draws a line on the image. The `save_image` function takes the image reference, width, height, and filename and saves the image as a PPM file.

In the `main` function, the program initializes the image, fills it with the background color, and then draws the bar chart by calling the `draw_filled_rect` and `draw_line` functions with specific parameters. The bars, icons, and percentages are drawn using these functions. After drawing the chart, the image is saved to a file with a specified filename.

![16_draw_bar_chart.ppm](resources/16_draw_bar_chart.jpg)

Figure 45\. 16_draw_bar_chart.ppm

Drawing a bar chart, take a look in source_code.zip: `16_draw_bar_chart.cpp`

## Draw a pie chart

The code is designed to create and output a simple pie chart. It first includes necessary headers such as iostream, fstream, tuple, vector, random, cmath, and algorithm to handle various functions required in the program. It then defines a set of functions for multiple calculations and operations.

The function `get_width_from_height` calculates the width of the pie chart based on the height. `get_margin_from_height` calculates the margin size for the chart based on the height. `get_index` returns the index of a pixel in the image vector given its x and y coordinates and the width of the image. The `calc_size` function calculates the chart size based on width, height, and margin.

The `stamp` function is responsible for stamping the image of a letter onto the pie chart, while the `clear_image` function sets the initial color of the pie chart to a light orange color. Functions `get_line_points,` `draw_font_M,` `draw_font_A,` `draw_font_R,` `draw_font_S,` `draw_font_V,` `draw_font_E,` `draw_font_N,` `draw_font_U,` and `draw_font_C` handle drawing of the individual letters on the pie chart using line segments and points. Each letter is represented by a set of coordinates and lines connecting them.

![16_draw_pie_chart.ppm](resources/16_draw_pie_chart.jpg)

Figure 46\. 16_draw_pie_chart.ppm

For the pie chart in PPM, take a look in source_code.zip: `16_draw_pie_chart.cpp`

## Draw a donut chart

The code provided is a C++ program that creates a donut chart with the letters “MARS” in the center. It uses a variety of functions to draw lines, circles, and characters on a 2D grid, ultimately constructing the desired image.

The program starts by including necessary headers and defining functions to perform operations such as calculating width and margin based on height, calculating the index of a 2D point in a 1D array, and clearing the image by setting a background color. Functions are also defined for drawing lines between two points and drawing filled circles.

Several functions are dedicated to drawing individual characters like `M, A, R, S.` These functions first define an array of points representing the outline of each character and then another array of lines connecting those points. Using the `get_line_points` function, lines are drawn between the specified points to create the shape of the characters.

The `draw_filled_circle` function takes in the center coordinates of a circle, its radius, and a color and then fills the circle with that color. The `draw_filled_circle2` function is a slightly modified version of `draw_filled_circle` without the margin parameter.

The `get_all_ys` function collects all the y-coordinates from a set of coordinates, sorts them, and removes duplicates. The `draw_line_coords` function is a helper function for drawing lines between two points and storing the resulting coordinates in a vector.

The `stamp` function places one image (letter) onto another image (donut chart) at a specified offset. The `draw_filled_circle_segment` function draws a filled segment of a circle, given the start and end angles.

Finally, the `main` function of the program sets up the dimensions and colors for the donut chart and uses the functions defined earlier to draw the diagram and letters. The resulting image is then saved as a PPM file, which can be opened with an image viewer that supports the format.

![16_draw_donut_chart.ppm](resources/16_draw_donut_chart.jpg)

Figure 47\. 16_draw_donut_chart.ppm

For the pie chart in PPM, take a look in source_code.zip: `16_draw_donut_chart.cpp`

## Draw a table

This C++ code is designed to draw a table, save the image as a PPM file, and demonstrate various graphics functions such as drawing lines, circles, and rectangles. It includes multiple functions to perform these tasks and a main function to tie them together.

First, the necessary libraries are included at the beginning of the code. The `get_width_from_height` function calculates the table’s width based on height, while the `get_margin_from_height` function calculates the margin based on the height. The `get_index` function calculates the index of a point in a one-dimensional vector based on its x and y coordinates and the given width.

The `calc_size` function calculates the size of the image, taking into account the width, height, and margin. The `clear_image` function initializes the image vector by setting the color of each pixel to a light brownish color. The `stamp` function stamps the input image (i.e., the letters) onto another image at a specified position.

The `get_line_points` function calculates the points along a line using Bresenham’s line algorithm, given the coordinates of the two endpoints and a color. This function is used in the `draw_font_*` functions, where each function (e.g., `draw_font_M, draw_font_A,` etc.) is responsible for drawing the respective letter using lines. Each function sets up arrays containing the coordinates of the points and lines that make up the letter and then calls `get_line_points` to calculate the points along each line.

The `draw_filled_circle` and `draw_filled_rect` functions draw filled circles and rectangles, respectively, on the image. The `save_image` function saves the image as a PPM file, given the image data, dimensions, and the output filename.

The draw function is used to draw points on the image. The points are drawn as filled circles with a specified line size. Finally, the `main` function initializes the image, sets the colors and dimensions for the table, and calls the various drawing functions to create the image. It then saves the image to a `table.ppm` file.

![16_draw_table.ppm](resources/16_draw_table.jpg)

Figure 48\. 16_draw_table.ppm

For the pie chart in PPM, take a look in source_code.zip: `16_draw_table.cpp`

## Draw a more advanced chart 1

The given function, `generate_noise_image,` is designed to create a noisy image by generating random grayscale pixel values. The noise image is represented as a vector of tuples, where each tuple contains three float values representing a pixel’s red, green, and blue channels.

The function takes two parameters: a reference to a `std::vector` of tuples named image, which will store the generated noise `image,` and two integers `width` and `height` representing the dimensions of the desired noise image. The function begins by defining a tuple named `color` and a float variable named `rndnum,` which will store random grayscale values.

Next, the function sets up a random number generator using the `std::random_device` and `std::mt19937` classes from the C++ standard library. The random number generator is configured to produce float values uniformly distributed between `0.0` and `1.0.`

The function then iterates through each pixel in the image using two nested loops. The outer loop iterates through the height of the image, while the inner loop iterates through the width. For each pixel, a random number is generated using the previously configured random number generator, and the `color` tuple is set to contain the random number for all three channels (red, green, and blue). This creates a grayscale color, as all channels have the same value. The `color` tuple is then assigned to the corresponding position in the `image` vector using the `get_index` function, which converts 2D coordinates (x, y) into a 1D index suitable for accessing the vector.

By the end of the function, the `image` vector will represent a noise image with the specified width and height, where each pixel is a randomly generated grayscale value.

![Step #1: 16_draw_market_size1.ppm](resources/16_draw_market_size1.jpg)

Figure 49\. Step #1: 16_draw_market_size1.ppm

The `generate_linear_gradient_image` function creates a linear gradient image by vertically blending two colors across the image. The resulting image is represented as a vector of tuples, where each tuple contains three float values representing a pixel’s red, green, and blue channels.

The function takes four parameters: a reference to a `std::vector` of tuples named image, which will store the generated gradient `image,` two tuples named `fcolor` and `tcolor` representing the starting and ending colors of the gradient, and two integers `width` and `height` representing the dimensions of the desired gradient image. The function begins by defining a tuple named `color` and double variables `resultRed,` `resultGreen,` and `resultBlue,` which will store the blended color values for each pixel.

Additionally, the function defines variables `fr,` `fg,` `fb,` `tr,` `tg,` and `tb` for storing the individual red, green, and blue components of the starting and ending colors. The `std::tie` function is used to unpack the `fcolor` and `tcolor` tuples into these separate variables.

The function then iterates through each row of the image using a loop that iterates through the height of the image. The function calculates the percentage of the current row’s total height for each row. This percentage is then used to blend the starting and ending colors for that row by computing the weighted average of the respective color components (red, green, and blue). The resulting blended color is stored in the `color` tuple using the `std::make_tuple` function.

Next, the function iterates through each column in the current row using a nested loop. For each pixel in the row, the `color` tuple containing the blended color for the current row is assigned to the corresponding position in the `image` vector using the `get_index` function, which converts 2D coordinates (x, y) into a 1D index suitable for accessing the vector.

By the end of the function, the `image` vector will represent a linear gradient image with the specified width and height, where the colors gradually blend from the starting color at the top of the image to the ending color at the bottom.

![Step #2: 16_draw_market_size2.ppm](resources/16_draw_market_size2.jpg)

Figure 50\. Step #2: 16_draw_market_size2.ppm

`blended_two_images` blends two images using a specified alpha value. It takes five input parameters: two vectors of tuples representing the two images’ colors, `width` and `height,` and a float value called `alpha.`

First, the function initializes three tuple variables, `color1` and `color2,` and three float variables, `r,` `g,` and `b.` The tuples represent colors from the first and second images, while the float variables represent the blended color components - red, green, and blue.

The function then uses two nested loops to iterate over the width and height of the images. The outer loop iterates over the height of the images, and the inner loop iterates over the width. Inside the inner loop, the function extracts the colors at the current position `(x, y)` from both images using the `get_index` function, which computes the index in the vector based on the x, y coordinates, and the width.

Next, the function calculates the blended color components (red, green, and blue) using the alpha value. The blending operation is performed by multiplying each color component of the second image by the alpha value and adding the product of the color component from the first image and (1.0 - alpha). This is done for all three-color components - red, green, and blue.

After calculating the blended color components, the function stores the blended color as a tuple in the first vector at the same position, `(x, y).` This overwrites the original color in the first image with the blended color. Once the loops have finished, the first vector will contain the resulting blended image.

![Step #3: 16_draw_market_size3.ppm](resources/16_draw_market_size3.jpg)

Figure 51\. Step #3: 16_draw_market_size3.ppm

`generate_radial_gradient_image` generates a radial gradient image using two input colors. It takes four input parameters: a vector of tuples representing the colors of the output image, two tuples representing the colors to create the gradient (from color and to-color), and the width and height of the image.

First, the function initializes several variables: color for storing the current `color` being computed, `pink` for a predefined color, `mask` for a vector of tuples to hold an intermediate mask, `distance from the center` for calculating the distance from the center of the image, and `resultRed,` `resultGreen,` and `resultBlue` for storing the resulting color components.

The function starts with two nested loops to iterate over the width and height of the image. Inside the inner loop, the function sets the initial values of the `mask` and `image` vectors at the current position `(x, y)` to the predefined `pink` color and the `from-color,` respectively.

The function then initializes several variables for drawing a circle using Bresenham`` s circle algorithm. It declares a lambda function drawline` `` used to draw horizontal lines at the specified positions. It loops over the circle, drawing lines for each quadrant, and updates the mask vector accordingly.

After completing the circle drawing, the function starts another pair of nested loops to iterate over the width and height of the image once more. Inside the inner loop, the function checks if the current position `(x, y)` in the `mask` vector does not equal the predefined `pink` color. If this condition is true, it calculates the distance from the center of the image and computes the resulting color components based on the distance and the input `from-color` and `to-color.` The function then assigns the calculated color to the `image` vector at the current position `(x, y).`

If the condition is false, meaning that the `mask` vector has the `pink` color at the current position `(x, y),` the function assigns the `to-color` to the `image` vector at the current position. This way, the final image vector will contain a radial gradient image generated using the input colors.

![Step #4: 16_draw_market_size4.ppm](resources/16_draw_market_size4.jpg)

Figure 52\. Step #4: 16_draw_market_size4.ppm

`generate_repeating_texture_image` generates a repeating texture image using an input color. The function takes three input parameters: a vector of tuples representing the colors of the output image, a tuple representing the color to create the texture, and the width and height of the image.

First, the function initializes a tuple called `bgcolor` to store a predefined background color. Then, it uses two nested loops to iterate over the width and height of the image. Inside the inner loop, the function sets the initial value of the `image` vector at the current position `(x, y)`` to the background color.

Next, the function defines two arrays named `arr` and `arr2,` which store the coordinates and indices of the line segments to draw the repeating texture pattern. The `arr` array contains 13 pairs of integers representing the x and y coordinates, and the `arr2` array includes 13 pairs of integers representing the indices of the line segments in the `arr` array.

The function then uses a loop to iterate over the 13-line segments, creating a tuple `coords` containing each line segment’s start and end coordinates. Inside the loop, the function calls the `draw_line` function, which draws the line segment on the `image` vector using the input `color,` `width,` and `height.` This process repeats for each line segment, resulting in a repeating texture pattern drawn on the image vector.

In summary, the `generate_repeating_texture_image` function creates a repeating texture image by drawing a series of line segments on an image vector using a predefined background color and an input color for the texture pattern. The function achieves this by iterating through a series of coordinates and line segment indices, drawing the texture pattern on the image vector using the `draw_line` function.

![Step #5: 16_draw_market_size5.ppm](resources/16_draw_market_size5.jpg)

Figure 53\. Step #5: 16_draw_market_size5.ppm

`render_repeating_texture_image` renders a repeating texture image by tiling a smaller image across a larger image. The function takes five input parameters: a vector of tuples representing the colors of the texture image, the width and height of the texture image (`tw` and `th),` a vector of tuples representing the colors of the output image, and the width and height of the output image (`iw` and `ih).`

The function uses two nested loops to iterate over the width and height of the output image. Inside the inner loop, the function calculates the corresponding position in the texture image using the modulo operator. The x and y coordinates of the output image are calculated as the remainder of the division of the x and y coordinates by (`tw - 1)` and (`th - 1),` respectively. This approach ensures that the texture image will be repeated across the output image, creating a tiled pattern.

Once the corresponding position in the texture image is determined, the function retrieves the color at that position using the `get_index` function, which computes the index in the vector based on the x and y coordinates and the texture image width (`tw).` The retrieved color is then assigned to the output image vector at the current position `(x, y)` using the `get_index` function with the output image width (`iw).`

![Step #6: 16_draw_market_size6.ppm](resources/16_draw_market_size6.jpg)

Figure 54\. Step #6: 16_draw_market_size6.ppm

`do_cookie_cut` extracts a rectangular region, a `cookie,` from a larger image. The function takes eight input parameters: a vector of tuples representing the colors of the input image, the width and height of the input image (w and h), a vector of tuples representing the colors of the output “cookie” image, the width and height of the “cookie” image (`cw` and `ch),` and the starting x and y coordinates (`startx` and `starty)` of the region to extract from the input image.

The function initializes two variables, `cx` and `cy,` which will store the x and y coordinates of the “cookie” image as it is being constructed. It then uses two nested loops to iterate over the rectangular region defined by the starting coordinates (`startx` and `starty)` and the width and height of the “cookie” image (`cw` and `ch).`

Inside the inner loop, the function retrieves the color from the input image at the current position `(x, y)` using the `get_index` function, which computes the index in the vector based on the x, y coordinates and the input image width (w). The retrieved color is then assigned to the “cookie” image vector at the position (cx, cy) using the get_index function with the “cookie” image width (`cw).`

After each inner loop iteration, the function increments the x-coordinate of the “cookie” image (`cx)` by 1\. After each iteration of the outer loop, the function increments the `y-coordinate` of the “cookie” image (`cy)` by one and resets the `x-coordinate` (`cx)` back to `0.`

![Step #7: 16_draw_market_size7.ppm](resources/16_draw_market_size7.jpg)

Figure 55\. Step #7: 16_draw_market_size7.ppm

`add_honeycomb` overlays a texture image onto an input image using an alpha channel image to control the blending. The function takes four input parameters: a vector of tuples representing the colors of the input image, a vector of tuples representing the colors of the alpha channel image, a vector of tuples representing the colors of the texture image, and the width and height of the images (w and h). The width and height are assumed to be the same for all three images.

First, the function initializes three color tuple variables (color1, color2, and color3) and a pink color tuple, which will be used later to determine if a pixel should be affected by the texture overlay.

The function then iterates over the width and height of the input image using two nested loops. Inside the inner loop, the function checks if the current pixel in the texture image is not equal to the pink color. If it is not pink, the texture overlay will affect the pixel.

Next, the function retrieves the colors from the input, texture, and alpha channel images at the current position `(x, y)` using the `get_index` function. The retrieved colors are assigned to the corresponding color tuple variables (color1, color2, and color3).

The function then calculates the blended color by multiplying the texture color (color2) with the alpha value (color3) and adding the input image color (color1) multiplied by the inverse of the alpha value (1.0f - color3). This process is done separately for the red, green, and blue channels, resulting in the final blended color components (ir, ig, and ib).

Finally, the blended color is assigned to the input image vector at the current position `(x, y)` using the `get_index` function. This process updates the input image with the texture overlay, effectively modifying the input image.

![Step #8: 16_draw_market_size8.ppm](resources/16_draw_market_size8.jpg)

Figure 56\. Step #8: 16_draw_market_size8.ppm

`stamp_cookie` passes a smaller image, a “cookie,” onto a larger image at a specified position. The function takes eight input parameters: a vector of tuples representing the colors of the input image, the width and height of the input image (w and h), a vector of tuples representing the colors of the “cookie” image, the width and height of the “cookie” image (cw and ch), and the starting x and y coordinates (startx and starty) of the position where the “cookie” image should be pasted onto the input image.

The function initializes two variables, `cx` and `cy,` which will store the x and y coordinates of the “cookie” image as it is being pasted onto the input image. It then uses two nested loops to iterate over the rectangular region defined by the starting coordinates (startx and starty) and the width and height of the “cookie” image (cw and ch).

Inside the inner loop, the function retrieves the color from the “cookie” image at the current position `(cx, cy)` using the `get_index` function, which computes the index in the vector based on the x, y coordinates and the “cookie” image width (cw). The retrieved color is then assigned to the input image vector at the position `(x, y)` using the `get_index` function with the input image width (w).

After each inner loop iteration, the function increments the x-coordinate of the “cookie” image (cx) by 1\. After each iteration of the outer loop, the function increments the y-coordinate of the “cookie” image (cy) by one and resets the x-coordinate (cx) back to 0.

![Step #9: 16_draw_market_size9.ppm](resources/16_draw_market_size9.jpg)

Figure 57\. Step #9: 16_draw_market_size9.ppm

The `draw_hexagon` function is designed to draw a hexagon with a specified color onto an image. The function takes eight parameters: a vector of tuples representing the colors of the input image, a tuple representing the color of the hexagon, the x and y coordinates of the hexagon`s center (centers and centery), the hexagons` radius, the width and height of the input image, and the “circle radius” (cradius) used for drawing the lines that make up the hexagon.

First, the function initializes some variables for calculating the hexagon’s vertices. It computes the upper-left corner of a bounding box around the hexagon, given by `(ux, uy).` It also initializes six points (pt1x, pt1y) to (pt6x, pt6y), all initially set to `(ux, uy).`

Next, the function calculates auxiliary variables (A, B, C) using trigonometric formulas involving the given hexagon radius and a constant PI value. The purpose of these calculations is to help determine the coordinates of the hexagon`s vertices.

Using the auxiliary variables, the function computes the coordinates of each hexagon vertex (pt1 to pt6). Each vertex`s x and y coordinates are updated based on the initial (ux,` uy)` position and the auxiliary variables.

The function then creates a vector of tuples called `points` that will be used to store the points along the lines that form the hexagon. The function generates the line points between each pair of adjacent vertices using the `get_line_points` function and stores the result in the `points` vector. Then, the `draw` function is called to draw the line using the points, the input image, the specified color, the image dimensions, and the “circle radius” (cradius). After drawing each line, the function clears the `points` vector to prepare it for the next line.

The `flood_fill` function is a simple recursive algorithm that replaces a specific color in an image with another color within a connected region. It takes six parameters: a vector of tuples representing the colors of the input image, the x and y coordinates of the starting point, tuples representing the old and new colors, and the width of the input image.

The function begins by checking if the color at the current coordinates (x, y) in the image equals the old color specified. If the colors match, it replaces the old color at that position with the new color. Then, the function recursively calls itself to perform the flood fill operation in four directions: right `x+1, y,` down `x, y+1,` left `x-1, y,` and up `x, y-1.`

This process continues until the function reaches pixels with a color different from the old color, effectively filling the connected region of pixels with the new color.

![Step #10: 16_draw_market_size10.ppm](resources/16_draw_market_size10.jpg)

Figure 58\. Step #10: 16_draw_market_size10.ppm

An image is being created with various hexagons drawn on it. The code starts by declaring a vector of tuples called `image8,` representing the colors in the image. The `image8` vector is resized to fit the image’s dimensions, which are calculated using the `calc_size(width, height)` function.

Next, the `fcolor` tuple is created using the `std::make_tuple` function with RGB values (1.0f, 1.0f, 1.0f), representing the color white. The `draw_hexagon` function is then called four times with different parameters, each drawing a hexagon on `image8` with the specified color, center coordinates, radius, image width, image height, and circle radius used for drawing the hexagon lines.

The first hexagon is drawn with its center at (784, 340) and a radius of 190\. The second hexagon is drawn with its center at (520, 500) and a radius of 143\. The third hexagon is drawn with its center at (730, 610) and a radius of 107\. Finally, the fourth hexagon is drawn with its center at (900, 680) and a radius of 76.

![Step #11: 16_draw_market_size11.ppm](resources/16_draw_market_size11.jpg)

Figure 59\. Step #11: 16_draw_market_size11.ppm

The `blend_hexagon` function is designed to blend two images, represented by the vectors `blend1` and `blend2,` based on a specific color condition. The function takes in four parameters: the two image vectors `blend1` and `blend2,` and the dimensions of the images, `width` and `height.`

First, the function initializes two color tuples, `color1` and `color2.` `color1` is initialized to (0.0f, 0.0f, 0.0f), which represents black, while `color2` is initialized to (1.0f, 1.0f, 1.0f), which means white. The function also initializes three float variables, `r,` `g,` and `b,` and an `alpha` variable with a value of 0.8f. The `alpha` value will blend the colors from the two images.

The function then iterates through all the pixels in the images using nested for-loops. For each pixel, it checks if the color of the corresponding pixel in `blend2` is equal to `color2,` which is white. If the condition is met, it retrieves the color of the corresponding pixel in `blend1` and blends it with black (0.0f, 0.0f, 0.0f), using the `alpha` value to determine the degree of blending.

After blending the colors, the result is stored in the `blend1` image at the corresponding pixel position. The blending is performed by multiplying each color component (red, green, and blue) of the color from `blend1` by the `alpha` value, then adding the product of the black color component and (1.0f - `alpha).` The new color tuple is created using the `std::make_tuple` function and is assigned to the corresponding pixel in the `blend1` image.

![Step #12: 16_draw_market_size12.ppm](resources/16_draw_market_size12.jpg)

Figure 60\. Step #12: 16_draw_market_size12.ppm

The `add_white_hexagon_border` function is designed to add a white border to an image based on the white pixels in another image. The function takes in four parameters: two image vectors, `image1` and `image2,` and the dimensions of the images, `width` and `height.`

First, the function initializes a color tuple named `color` with the values (1.0f, 1.0f, 1.0f) representing the color white.

Next, the function iterates through all the pixels in the images using nested for-loops. For each pixel, it checks if the color of the corresponding pixel in `image2` is equal to `color,` which is white. If the condition is met, it sets the color of the corresponding pixel in `image1` to white.

![Step #13: 16_draw_market_size13.ppm](resources/16_draw_market_size13.jpg)

Figure 61\. Step #13: 16_draw_market_size13.ppm

The `draw_label_lines` function is designed to draw multiple lines on an image with a specific color and thickness. The function accepts five parameters: a reference to the image vector, a reference to the color tuple, the width and height of the image, and the thickness of the lines represented as radius.

First, the function initializes a `coords` tuple, which will store the coordinates of the starting and ending points of the lines to be drawn. It also initializes a `points` vector, holding the points on the line.

![Step #14: 16_draw_market_size14.ppm](resources/16_draw_market_size14.jpg)

Figure 62\. Step #14: 16_draw_market_size14.ppm

This code defines a function called `draw_labels` that takes three arguments: a reference to a vector of tuples called `image,` a reference to a tuple called `color,` and two integers called `width` and `height.` The function uses a specified color to draw labels on an image.

The image is represented by a vector of tuples, where each tuple contains three floating-point values representing a pixel’s red, green, and blue channels. The `color` tuple also contains three floating-point values that represent the red, green, and blue channels of the desired color for the labels.

The `draw_labels` function begins by defining a hard-coded label called `lable_10,` a series of 0s and 1s that represent the pixel values of an image. This label was created in a graphics application and converted to a binary format for use in this function. The 0s represent transparent pixels, while the 1s represent the color specified by the `color` argument.

The purpose of the function is to draw this `lable_10` on the `image` using the specified `color,` `width,` and `height.` However, the provided code only defines the `lable_10` data and does not include the necessary steps to draw the label on the image. The actual drawing process would involve iterating through the lable_10 data and, for each one encountered, setting the corresponding pixel in the `image` vector to the specified `color.`

![Step #15: 16_draw_market_size15.ppm](resources/16_draw_market_size15.jpg)

Figure 63\. Step #15: 16_draw_market_size15.ppm

For the pie chart in PPM, take a look in source_code.zip: `16_draw_market_size.cpp`

## Draw a more advanced chart 2

The code is designed to create a noisy image. It comprises two main parts: variable declarations and initialization and a function definition. The code first defines a vector of tuples called `image1` to store the noise image data. Each tuple contains three float values that represent a pixel’s red, green, and blue channels. The width and height of the image are then set to 1600 and 900 pixels, respectively. The `image1` vector is resized to the appropriate size using the `calc_size(width, height)` function.

The `generate_noise_image` function is defined to create the noise image. It refers to a vector of tuples (`image),` as well as the width and height of the image as its parameters. The function generates a random grayscale color for each pixel in the image using a random number generator (`std::mt19937)` seeded by a random device (`std::random_device).` The random number generator is used to create a uniform distribution of float values between 0.0 and 1.0, representing the grayscale color’s intensity.

In the nested for loop, the code iterates through each image pixel. It generates a random number (`rndnum)` using the uniform distribution and the random number generator. This random number is then used to create a grayscale color by setting the red, green, and blue channels to the same value (`rndnum).` The color is stored as a tuple and assigned to the corresponding index in the `image` vector using the `get_index(x, y, width)` function. This process is repeated for all the pixels in the image, resulting in a noisy image.

![Step #1: 16_draw_investment1.ppm](resources/16_draw_investment1.jpg)

Figure 64\. Step #1: 16_draw_investment1.ppm

This C++ code generates a linear gradient image. It consists of two main parts: the declaration and initialization of variables and the definition of the `generate_linear_gradient_image` function.

In the first part of the code, a vector of tuples called `image2` is created to store the linear gradient image data. Each tuple holds three float values representing a pixel’s red, green, and blue channels. The width and height of the image are assumed to be already defined with values of 1600 and 900 pixels, respectively. The `image2` vector is resized to the appropriate size using the `calc_size(width, height)` function. The code then defines two tuples, `fcolor` and `tcolor,` representing the starting and ending colors of the gradient, and calls the `generate_linear_gradient_image` function.

The `generate_linear_gradient_image` function is defined to create the linear gradient image. It takes a reference to a vector of tuples (`image),` references to the starting and ending colors (`fcolor` and `tcolor),` and the width and height of the image as its parameters. The function calculates the color of each pixel in the image by interpolating between the starting and ending colors based on the pixel`s position.

First, the red, green, and blue channels of the starting and ending colors are extracted using the `std::tie` function. Then, the code iterates through the height of the image using a for loop. In each iteration, it calculates the interpolation percentage based on the current vertical position of the pixel. The interpolated color’s red, green, and blue channels are calculated by linearly interpolating between the corresponding channels of the starting and ending colors using the estimated percentage. The interpolated color is then stored as a tuple.

The code iterates through the image’s width in the inner for loop. For each pixel in the current row, the code assigns the interpolated color to the corresponding index in the `image` vector using the `get_index(x, y, width)` function. This process is repeated for all the rows in the image, ultimately generating a linear gradient image.

![Step #2: 16_draw_investment2.ppm](resources/16_draw_investment2.jpg)

Figure 65\. Step #2: 16_draw_investment2.ppm

`blended_two_images` takes two input images and blends them based on a specified alpha value. The images are passed as vectors of tuples (float, float, float), representing each pixel’s red, green, and blue (RGB) color values. The function also takes the width and height of the images and an alpha value, which is a float between 0 and 1.

The function starts by initializing three tuples named `color1` and `color2,` and three float variables `r,` `g,` and `b` that will be used to store the RGB values of each pixel in the two images and the resultant blended image. Two nested loops are then used to iterate through each pixel in the input images. The outer loop iterates through the rows (height), while the inner loop iterates through the columns (width).

For each pixel, the corresponding color values are retrieved from the input images using the `get_index` function and stored in `color1` and `color2.` The blended image’s red, green, and blue values are calculated by multiplying the corresponding color values from the second image by the alpha value and the color values from the first image by (1 - alpha), then summing them. These blended RGB values are stored in the first image vector using the `get_index` function again.

Once the loops have finished iterating through all the pixels, the function effectively modifies the first input image vector to store the blended image. In contrast, the second input image vector remains unchanged.

![Step #3: 16_draw_investment3.ppm](resources/16_draw_investment3.jpg)

Figure 66\. Step #3: 16_draw_investment3.ppm

`generate_radial_gradient_image` creates a radial gradient image with a specified size and two colors. The radial gradient image is stored as a vector of tuples (float, float, float), representing each pixel’s red, green, and blue (RGB) color values.

The function takes the following parameters: a reference to the image vector regarding two color tuples (fcolor and tcolor) and the width and height of the image. The function starts by initializing some variables: `color` (a tuple to store the current pixel`s color), pink``(a pre-defined color tuple),mask``(a vector to hold a circular mask),distanceFromCenter,` `resultRed,` `resultGreen,``` andresultBlue.` ``

The first nested for loops fill the `mask` and `image` vectors with the `pink` color and `fcolor,` respectively. Then, the function calculates the midpoint of the image `x0, y0` and initializes variables `d,` `xx,` and `yy` to draw a circle using Bresenham`s circle algorithm.

A lambda function `drawline` is defined within the function to draw horizontal lines between two points `sx, ex` at the given `y-coordinate` `ny` in the `mask` vector. The while loop uses Bresenham`s circle algorithm to create a circular mask by drawing lines in the mask``` vector using thedrawline` `` function.

Finally, another set of nested loops iterates through each pixel in the image. For each pixel, it checks if the corresponding mask pixel is not equal to the `pink` color. If so, it calculates the distance from the center of the image to the current pixel. It computes the interpolated color values based on the distance and input colors `fcolor` and `tcolor.` The resulting color tuple is assigned to the `image` vector at the current position. If the mask pixel equals the `pink` color, the `tcolor` is assigned directly to the `image` vector.

![Step #4: 16_draw_investment4.ppm](resources/16_draw_investment4.jpg)

Figure 67\. Step #4: 16_draw_investment4.ppm

`generate_repeating_texture_image` generates a repeating texture pattern with a given width, height, and color. The texture image is stored as a vector of tuples (float, float, float), representing each pixel’s `red,` `green,` and `blue` (RGB) color values.

The function takes the following parameters: a reference to the image vector, a reference to the color tuple, and the width and height of the image. It begins by initializing a background color tuple named `bgcolor` to be pink. Then, using two nested loops, it fills the `image` vector with this background color.

The function defines two integer arrays, `arr` and `arr2,` with hardcoded coordinates and indices representing the positions and connections of points in the pattern. The `coords` tuple is initialized to store the coordinates of the line endpoints in the pattern.

Next, using a for loop, the function iterates through the 13 hardcoded points. During each iteration, it creates a `coords` tuple using the coordinates from the `arr` array based on the indices found in the `arr2` array. The `draw_line` function is then called with the `image` vector, `coords` tuple, input color, width, and height as parameters. This function draws lines between the coordinates specified by the `coords` tuple in the image vector using the input color.

![Step #5: 16_draw_investment5.ppm](resources/16_draw_investment5.jpg)

Figure 68\. Step #5: 16_draw_investment5.ppm

`render_repeating_texture_image` takes a texture image and renders it repeatedly across a larger image. The texture and the larger image are stored as vectors of tuples (float, float, float), representing each pixel’s `red,` `green,` and `blue` (RGB) color values.

The function takes the following parameters: a reference to the texture vector, the width and height of the texture `tw, th,` the image vector, and the width and height of the image `iw, ih.` It uses two nested loops to iterate through each pixel in the larger image. For each pixel, the function retrieves the corresponding color value from the texture vector using the `get_index` function, with the x and y coordinates of the pixel modulo (tw-1) and (th-1), respectively. This ensures that the texture is repeated across the entire image. The retrieved color value is then assigned to the corresponding pixel in the image vector.

![Step #6: 16_draw_investment6.ppm](resources/16_draw_investment6.jpg)

Figure 69\. Step #6: 16_draw_investment6.ppm

`do_cookie_cut` extracts a rectangular section from a source image and stores it in another image, often called `cookie-cutting.` The source image and the resulting image are stored as vectors of tuples (float, float, float), representing each pixel’s `red,` `green,` and `blue` (RGB) color values.

The function takes the following parameters: a reference to the source image vector, the width and height of the source image `w, h,` a reference to the resulting image vector, the width and height of the resulting image `cw, ch,` and the starting x and y coordinates `startx, starty` of the rectangular section to be extracted from the source image. It initializes two variables, cx, and cy, to keep track of the current x and y coordinates in the resulting image.

The function uses two nested loops to iterate through the rectangular section of the source image, starting from the specified starting coordinates `startx, starty` and covering the width and height of the resulting image `cw, ch.` Each pixel in the section copies the color value from the source image to the corresponding position in the resulting image, using the `get_index` function to convert the 2D coordinates to a linear index. The cx and cy variables are updated to move through the resulting image.

![Step #7: 16_draw_investment7.ppm](resources/16_draw_investment7.jpg)

Figure 70\. Step #7: 16_draw_investment7.ppm

`add_honeycomb` combines three images: a base image, an alpha image, and a texture image. The base image and the texture image are combined using the red channel of the alpha image as a weight. All three images are stored as vectors of tuples (float, float, float), representing each pixel’s `red,` `green,` and `blue` (RGB) color values.

The function takes the following parameters: references to the base image vector, alpha image vector, texture image vector, and the width and height of the images `w, h.` It initializes several tuple variables to store the color values of the three images at each pixel and a pink color tuple (1.0f, 0.0f, 1.0f) to check against the texture image.

Using two nested for loops, the function iterates through each pixel of the images. If the color value of the texture image at the current pixel is not pink, the function retrieves the color values of the base, texture, and alpha images at the current pixel. It then calculates the new red, green, and blue color values for the base image by interpolating between the texture and base images` color values using the red channel of the alpha image as a weight. The resulting color value is assigned back to the base image at the current pixel.

![Step #8: 16_draw_investment8.ppm](resources/16_draw_investment8.jpg)

Figure 71\. Step #8: 16_draw_investment8.ppm

`stamp_cookie` places a smaller `cookie` image onto a larger base image at a specified position. The base image and the cookie image are stored as vectors of tuples (float, float, float), representing each pixel’s red, green, and blue (RGB) color values.

The function takes the following parameters: references to the base image vector, its width, and height (w, h), the cookie image vector, its width and height (cw, ch), and the starting x and y coordinates (startx, starty) for placing the cookie image onto the base image.

The function initializes two integer variables, cx, and cy, to keep track of the current position within the cookie image. It then uses two nested loops to iterate through each pixel of the area where the cookie image will be placed on the base image.

For each pixel in the specified area, the function retrieves the color value from the cookie image at the current cx and cy coordinates and assigns it to the base image at the current x and y coordinates. The cx variable is incremented for each iteration of the inner loop, while the cy variable is incremented for each outer loop iteration. After the inner loop is completed, the cx variable is reset to 0 to start processing the next row of the cookie image.

![Step #9: 16_draw_investment9.ppm](resources/16_draw_investment9.jpg)

Figure 72\. Step #9: 16_draw_investment9.ppm

The code creates an image of a doughnut shape with various shades of gray and white and some additional labels. The doughnut consists of filled wedges and lines drawn on a base image.

The base image, `image7,` is initialized as a vector of tuples (float, float, float), representing each pixel’s red, green, and blue (RGB) color values. The base image is then resized to the desired width and height.

The image is first cleared to a solid color (magenta) using the `clear_image` function. Next, the doughnut shape is constructed by drawing filled wedges and lines with shades of gray and white. The `draw_filled_wedge` function is used to draw the filled wedges, while the `draw_line` function is used to draw the lines. Each function takes the image, coordinates, and color information as input.

Finally, the `draw_labels` function adds labels to the image. This function takes the image, color (white), width, and height as input.

![Step #10: 16_draw_investment10.ppm](resources/16_draw_investment10.jpg)

Figure 73\. Step #10: 16_draw_investment10.ppm

The code adds the previously created doughnut shape to the `image1` by copying the non-magenta pixels from `image7` to `image1.` The magenta color (1.0f, 0.0f, 1.0f) is used as a background color in `image7` and is not copied to `image1.`

The code first defines the magenta color as `fcolor,` which will be used to identify the background pixels that should not be copied.

Then, two nested loops iterate over the height and width of the images. For each pixel coordinate (x, y), the code checks if the pixel in `image7` is not magenta (i.e., not equal to `fcolor).` If the condition is true, the non-magenta pixel from `image7` is copied to the corresponding position in `image1.`

In summary, the code adds the doughnut shape from `image7` to `image1` by copying only the non-magenta pixels from `image7` to their corresponding positions in `image1.`

![Step #11: 16_draw_investment11.ppm](resources/16_draw_investment11.jpg)

Figure 74\. Step #11: 16_draw_investment11.ppm

For the PPM pie chart, look at source_code.zip: **16_draw_investment.cpp**

## Collaboration

We can use 2D charts and diagrams to help us understand and solve problems collaboratively. For example, we can use a chart to visualize the relationships between different elements in a problem or a diagram to explore the potential solutions to a problem.

2D charts and diagrams are also helpful for communicating our ideas to others. We can use them to explain our thinking process or present our findings clearly and concisely.

When working with 2D graphs and diagrams, knowing the different types of data they can represent is vital. For instance, some charts are better suited for displaying quantitative data, while others are more effective for visualizing qualitative data. Additionally, we must be careful when interpreting data from 2D graphs and diagrams, as they can sometimes be misleading.

Despite these limitations, 2D graphs and diagrams are powerful tools that can help us think more creatively and solve problems more effectively. We can learn to use them in various ways to improve our collaborative problem-solving skills with some practice.

Peacock chart in PPM, take a look in source_code.zip: `17_colab_peacock.cpp`

![peacock graph](resources/17_colab_peacock.jpg)

Figure 75\. peacock graph

## Investigation

There is a reason that businesses, law enforcement agencies, and military intelligence use data visualization when investigating crimes or irregularities - it works. By taking large data sets and representing them in an easily digestible format, investigators can quickly identify patterns and relationships that would otherwise be difficult to spot. The correct data can help investigators determine what happened and who was involved.

Also, for a security incident, a simple graph can give you vital information, such as when and how much activity happened. Also, what kind of activity is in the log?

![Investigating log](resources/18_investigation_logs.jpg)

Figure 76\. Investigating log

* * *

![](resources/moreexamples.jpg)

Figure 77

# More Advanced Examples

## Concentric Hexagons

**Source code**: `18_concentric_hexagons.cpp`

![Concentric Hexagons](resources/18_concentric_hexagons.jpg)

Figure 78\. Concentric Hexagons

![Concentric Filled Hexagons](resources/18_concentric_filled_hexagons.jpg)

Figure 79\. Concentric Filled Hexagons

![Concentric Textured Hexagons](resources/18_concentric_textured_hexagons.jpg)

Figure 80\. Concentric Textured Hexagons

### Introduction

Concentric hexagons stand as a fascinating and visually appealing concept when delving into the world of geometric shapes in programming. This chapter explores the creation and manipulation of concentric hexagons using C++. This journey highlights the aesthetic potential of programming and underscores the geometric and algorithmic thinking integral to computer graphics.

### Understanding Hexagons in Graphics

Hexagons are six-sided polygons widely used in various fields, from graphic design to architectural planning. Computer graphics offer a unique approach to tiling and patterning due to their regular shape and tiling properties. Concentric hexagons, which consist of multiple hexagons sharing the same center, create captivating patterns and are an excellent subject for exploring geometric calculations and rendering in C++.

### Implementing Hexagons in C++

To create hexagons in C++, we define their geometric properties, such as the center point and radius. The implementation involves calculating the vertices of a hexagon and rendering them on a 2D plane. We use trigonometric functions from the C++ Standard Library to calculate the points on the circumference of a circle and then connect these points to form a hexagon.

### Drawing a Single Hexagon

We begin with the simple task of drawing a single hexagon. The `drawHexagon` function calculates the vertices of the hexagon based on the center point and radius and then draws straight lines connecting these vertices. This basic procedure forms the foundation for creating more complex hexagonal patterns.

### Generating Concentric Hexagons

Building upon the single hexagon, we extend our code to generate concentric hexagons. This involves drawing multiple hexagons with the same center but increasing radii. The visual effect is a series of nested hexagons, each larger than the previous. This technique demonstrates the geometric principles and creates an opportunity to explore looping structures and incremental calculations in C++.

### Filling Hexagons with Color and Texture

We explore filling the hexagons with solid colors and textures to add depth and visual interest. The `drawFilledHexagon` function fills a hexagon with a specified color, while `drawFilledHexagonWithTexture` uses a texture image to load the hexagon, creating a rich, detailed appearance. These functions illustrate using pixel manipulation and image processing techniques in C++.

### Practical Application: Creating a Hexagonal Pattern

We apply these concepts to create a complete hexagonal pattern. This pattern consists of concentric hexagons with alternating fills and textures, demonstrating the practical application of the concepts discussed. This exercise not only serves as a coding practice but also as an artistic exploration in the realm of computer graphics.

### Challenges and Solutions in Rendering Hexagons

Rendering hexagons, mainly when filled or textured, presents its challenges. Efficiently determining which pixels lie inside a hexagon requires careful geometric calculations. We address these challenges by discussing algorithms like point-in-polygon tests and efficient looping through pixel grids.

### Advanced Techniques: Dynamic Hexagonal Patterns

As an advanced topic, we explore creating dynamic hexagonal patterns, where properties like size, color, and texture change over time or in response to user input. This opens the door to interactive graphics and animations, highlighting the interplay between geometry, user interaction, and rendering in C++.

### About the code

The code in `18_concentric_hexagons.cpp` utilizes the `ppmpp.hpp` graphics library to generate images of concentric hexagons. The program is written in C++ and is divided into several functions, each serving a specific purpose in the drawing process.

At the start, the `isInsideTriangle` function determines if a given point lies within a triangle. This is crucial for the hexagon drawing process, as the hexagons are filled by deciding if a point lies within any triangles that compose the hexagon. The function uses barycentric coordinates to perform this check.

Next, `drawFilledHexagonWithTexture` and `drawFilledHexagon` functions are provided to draw filled hexagons. The former serves the hexagon with a texture, while the latter fills it with a solid color. Both functions start by computing the corners of a hexagon based on the given center and radius. Then, they iterate over a bounding box around the hexagon, using the `isInsideTriangle` function to check if a point is inside the hexagon. If it is, the point is colored accordingly.

The `drawHexagon` function is more straightforward, designed to outline a hexagon. It calculates the hexagon’s vertices and draws lines between successive points to form its shape.

The program begins in the `main` function by creating two images and defining some color palettes. The first primary task is to draw concentric hexagons. This is done by repeatedly calling `drawHexagon,` each time with a different radius, to create the effect of concentric shapes.

The program then proceeds to draw filled concentric hexagons. This is achieved using `drawFilledHexagon,` which colors each hexagon with different shades from the defined color palette. The radius is decreased in each iteration to create the concentric effect.

Finally, the program draws concentric hexagons with a textured fill. This uses the `drawFilledHexagonWithTexture` function, which uses the second image (`img2)` as the texture source. The texture offset is increased with each iteration, creating a dynamic textured appearance.

This program’s use of gradients, textures, and geometric calculations demonstrates a sophisticated approach to 2D graphics programming. The choice of hexagons, a complex shape compared to regular polygons like triangles or rectangles, adds an exciting challenge and showcases the capabilities of the `ppmpp` library and C++ in creating detailed and visually appealing graphics.

### Conclusion

Concentric hexagons represent a beautiful intersection of geometry, art, and programming. Through this chapter, programmers gain the technical know-how to render hexagons in C++ and an appreciation for the aesthetic possibilities of programming. This exploration paves the way for more complex graphical projects and inspires creative applications of geometric concepts in computer graphics.

### Exercises

To deepen your understanding and enhance your skills in rendering hexagons with C++, consider the following exercises:

1.  **Create Different Hexagonal Layouts**: Experiment with different arrangements of hexagons, such as grid layouts or random distributions, and observe the resulting patterns.

2.  **Experiment with Color Schemes**: Try applying different color schemes to the concentric hexagons, such as gradients or random color choices, to create visually appealing designs.

3.  **Integrate Mathematical Functions**: Use mathematical functions to vary the properties of the hexagons, such as size or color, based on mathematical equations or noise functions.

4.  **Animate the Hexagons**: Implement a simple animation where the hexagons grow, shrink, or change color over time, practicing the basics of animation in C++.

5.  **Hexagon Collision Detection**: Write a function to detect when a point or another shape collides with a hexagon, exploring geometric collision detection concepts.

6.  **Explore 3D Hexagons**: Extend the concept to 3D by creating a hexagonal prism, introducing basic 3D rendering concepts in C++.

7.  **User-Interactive Hexagons**: Implement user interaction where clicking or hovering over a hex

* * *

## Triangle Grid

**Source code**: `19_triangle_grid.cpp`

![Original Image](resources/19_photo.jpg)

Figure 81\. Original Image

![Triangle Grid Image](resources/19_triangle_grid.jpg)

Figure 82\. Triangle Grid Image

### Introduction

Triangles are fundamental shapes in computer graphics, forming the basis for complex shapes and patterns. This chapter delves into creating a triangle grid in C++ programming. This exploration not only enhances understanding of basic geometric computations but also introduces more complex graphical concepts such as tiling and pattern generation.

### Understanding Triangles in Computer Graphics

Triangles are the simplest polygons that can be used to form any 2D shape. Their simplicity makes them a popular choice in various graphical applications. Triangles can create visually striking patterns and textures when arranged in a grid. This chapter focuses on generating a grid of triangles and manipulating their properties to create exciting visuals.

### Implementing Triangle Grid in C++

Creating a triangle grid in C++ involves calculating the coordinates of each triangle’s vertices and rendering them on a 2D plane. We use simple arithmetic and looping structures to calculate these points and draw the triangles. The `averageTriangleColor` function is a crucial component that calculates the average color of the pixels within a triangle, allowing us to fill each triangle with a color representative of an underlying image.

### Drawing a Triangle

The fundamental step in creating a triangle grid is drawing a single triangle. We discuss how to determine the vertices of a triangle and use the `drawFilledTriangle` function to render it on the screen. This function fills the triangle with a solid color, providing a basis for more complex operations.

### Generating a Grid of Triangles

Building upon the single triangle, we extend our code to generate a grid of triangles. This involves systematically placing triangles next to each other, ensuring they fit together without overlapping or leaving gaps. We explore looping constructs and coordinate calculations essential to creating a seamless grid.

### Coloring Triangles Based on an Image

To add more depth to the grid, we discuss filling each triangle with a color-averaged from a specific area of an image. This technique demonstrates how to sample colors from an image and apply them to geometric shapes, a method commonly used in image processing and pattern generation in computer graphics.

### Practical Application: Creating a Triangle-Based Artwork

We apply these concepts to create a piece of artwork where a grid of triangles represents an image, giving it a unique, mosaic-like appearance. This practical example serves as a coding exercise and an exploration of the artistic potential of programming.

### Challenges and Solutions in Triangle Grids

Creating a triangle grid presents challenges, particularly in accurately calculating vertex positions and efficiently sampling image colors. We address these challenges by discussing geometric concepts and optimization techniques in C++.

### Advanced Techniques: Dynamic Triangle Patterns

As an advanced topic, we explore creating dynamic triangle patterns, where properties like size, color, or orientation change over time or in response to user input. This introduces the concepts of animation and interactivity in the context of geometric rendering.

### About the code

The `19_triangle_grid.cpp` program, written in C++, uses the `ppmpp.hpp` graphics library to create a grid of triangles on an image, each filled with the average color of the corresponding area on another image. This program demonstrates a creative way to use geometric shapes and color averaging to create a visually appealing transformation of an image.

Firstly, the program includes necessary headers and the `ppmpp.hpp` library, which is essential for image processing. The `averageTriangleColor` function is a critical component of this program. It calculates the average color within a given triangle on the image. This function works by iterating over the pixels within the triangle, summing up their red, green, and blue values, and then dividing these sums by the total number of pixels to get the average color. This process involves sorting the triangle’s vertices and using an efficient scanline algorithm to iterate over the triangle’s area, ensuring that every pixel within the triangle is considered.

In the `main` function, the program starts by loading an image (named `19_photo.ppm)` and creating a new image of the same size. The new image’s pixels are initially set to the average color of the entire source image. The program then divides the image into a grid, with the number of cells in the grid determined by the `gridSize` variable.

For each cell in the grid, the program calculates the coordinates of the vertices of two triangles that divide the cell into two equal parts. These triangles are then filled with the average color of their corresponding area in the source image. This is achieved by calling each triangle’s `averageTriangleColor` function to determine its average color and then using the `drawFilledTriangle` function to draw the triangle on the new image.

Finally, after processing the entire grid, the program writes the resulting image to a file named `19_triangle_grid.ppm.` The output is a fascinating transformation of the original image, where each grid cell is represented by two triangles, each filled with the average color of the corresponding area in the source image. This technique creates a unique mosaic-like effect, showcasing an interesting blend of geometric patterns and color averaging in image processing.

### Conclusion

Triangle grids offer a unique combination of geometric rigor and creative expression in C++. Through this chapter, programmers learn the technical aspects of creating and manipulating triangles and explore the artistic applications of these geometric shapes. The skills and knowledge acquired here serve as a foundation for more complex graphical projects and open the door to creative programming.

### Exercises

To deepen your understanding and enhance your skills in creating triangle grids with C++, consider the following exercises:

1.  **Experiment with Different Grid Sizes**: Change the grid size and observe how it affects the overall appearance of the triangle pattern. Experiment with both small and large grid sizes.

2.  **Vary Triangle Orientation**: Modify the code to alternate the orientation of triangles within the grid, creating a more complex pattern.

3.  **Apply Gradient Coloring**: Instead of averaging colors from an image, apply a gradient color scheme across the grid, transitioning smoothly from one color to another.

4.  **Animate the Triangle Grid**: Implement simple animations, such as changing the color or size of the triangles over time, to create a dynamic pattern.

5.  **Interactive Triangle Grid**: Make the grid-interactive by changing the color of triangles based on user input, such as mouse position or clicks.

6.  **Create a 3D Triangle Grid**: Extend the concept to 3D space by creating a grid of triangular prisms, introducing basic 3D rendering concepts in C++.

7.  **Triangle Grid as Image Filter**: Use the triangle grid to filter images, creating artistic variations of photographs or other images.

8.  **Randomize Triangle Properties**: Implement randomization in triangle size, color, or position to create a more organic and less uniform pattern.

9.  **Generate Artistic Patterns**: Use the triangle grid to generate specific artistic patterns, such as quilts or mosaics, by carefully selecting colors and arranging triangles.

10.  **Optimize Rendering Performance**: Explore optimization techniques for rendering many triangles efficiently, such as buffering or parallel processing.

* * *

## Color Quantization

**Source code**: `20_color_quantizer.cpp`

![Original Image](resources/20_colorquantizer.jpg)

Figure 83\. Original Image

![Quantized to 255 color palette](resources/20_colorquantizer_quantized.jpg)

Figure 84\. Quantized to 255 color palette

### Introduction

Color quantization is a fundamental technique in image processing that reduces the number of colors in an image. This chapter explores the implementation of color quantization in C++ programming, offering insights into this vital concept’s theoretical and practical aspects.

### Understanding Color Quantization

Color quantization involves mapping a large set of colors to a smaller one, typically in a way that preserves the appearance of the original image. This process is crucial in scenarios where color limitations are necessary, such as in specific display systems or for image compression. By implementing color quantization, we delve into digital image processing, color theory, and algorithm optimization in C++.

### Implementing Color Quantization in C++

In our C++ implementation, we create a `ColorQuantizer` class that handles the quantization process. The class reads an image, performs K-means clustering to reduce the color palette, and then applies Floyd-Steinberg dithering to maintain the image’s visual quality. This approach quantizes the colors and subtly spreads the quantization error over neighboring pixels to avoid noticeable color banding.

### The K-means Clustering Algorithm

K-means clustering is used to partition colors into a predefined number of clusters (or palettes), minimizing the distance between colors in the same cluster. We discuss implementing this algorithm in C++, focusing on initializing color clusters, assigning hues to the nearest sets, and recalculating cluster centers.

### Floyd-Steinberg Dithering

After reducing the color palette, we apply Floyd-Steinberg dithering, an error diffusion algorithm. This technique distributes the quantization error of a pixel to its neighboring pixels, preserving the image’s overall appearance despite the reduced color palette. We explore the implementation of this algorithm and how it enhances the final quantized image.

### Practical Application: Creating a Quantized Image

Using the `ColorQuantizer` class, we take an input image, perform color quantization, and generate a new image with a reduced color palette. This practical example demonstrates the power of color quantization in transforming images and provides a real-world application of the algorithms discussed.

### Challenges and Solutions in Color Quantization

Color quantization comes with challenges, such as choosing the correct number of colors for the palette and efficiently processing large images. We discuss strategies to overcome these challenges, including optimization techniques and best practices in C++ programming.

### Advanced Techniques: Customizing the Quantization Process

Moving beyond basic quantization, we explore ways to customize the process. This includes varying the number of colors in the palette, experimenting with different clustering algorithms, and adjusting the dithering process to achieve various artistic effects.

### About the code

In `20_color_quantizer.cpp,` the focus is on reducing the color palette of a 24-bit image to a smaller, 256-color palette and then applying dithering to maintain the image’s visual quality. This is a common technique in computer graphics for creating images with a limited color palette but retaining a semblance of the original’s color depth and detail.

The code begins by defining a `Color` struct, which holds red, green, and blue values as doubles. It also includes overloaded operators for comparison, which is essential for sorting and comparing color values.

The core of the program is encapsulated in the `ColorQuantizer` class. This class takes a filename as an argument and performs several steps to quantize the image’s color. The `readPPMP6` function reads an image in the PPM file’s P6 (binary) format, storing each pixel’s color in the `imgsrc` vector.

The `kmeansQuantization` function is where the color quantization occurs. It employs the k-means clustering algorithm, a popular method in machine learning for grouping data into k number of clusters. Here, it’s used to reduce the colors in the image to 256 distinct sets (or colors). This step involves initializing a palette of random colors and then iteratively refining this palette to represent the most common colors in the image.

After quantization, the `floydSteinbergDithering` function is called. This method applies the Floyd-Steinberg dithering algorithm to the quantized image. Dithering is a technique used in computer graphics to create the illusion of color depth in images with limited color palettes. Distributing the quantization error to neighboring pixels in a specific pattern helps to reduce the appearance of color banding and gives a more natural look to the final image.

The program also includes functions to write the quantized image data (`writePPMP6),` the color palette (`writePalette),` and the indexed image (`writeIndexedImage).` The indexed image represents each pixel of the quantized image as an index into the color palette, a common format for images with limited color palettes.

Finally, in the `main` function, an instance of `ColorQuantizer` is created, triggering the quantization process. This resulted in a new image with a reduced color palette and applied dithering, closely resembling the original image despite significantly fewer colors. This technique is beneficial in scenarios with limited memory, such as old video games or embedded systems, where storing full 24-bit color images is not feasible.

### Conclusion

Color quantization is a fascinating area of computer graphics and image processing. This chapter provides a comprehensive guide to implementing color quantization in C++, from reading and writing images to the intricacies of K-means clustering and dithering algorithms. The knowledge and skills acquired here are invaluable for any programmer working with images and graphics in C++.

### Exercises

To enhance your understanding and skills in color quantization with C++, consider the following exercises:

1.  **Experiment with Different Color Palettes**: Try quantizing images with different numbers of colors in the palette and observe the effects on the output image.

2.  **Implement Alternative Clustering Algorithms**: Beyond K-means, explore other clustering algorithms like DBSCAN or hierarchical clustering for color quantization.

3.  **Vary Dithering Techniques**: Experiment with different dithering algorithms, such as Atkinson or Burkes, and compare their effects to Floyd-Steinberg dithering.

4.  **Quantize Images with Unique Color Schemes**: Apply color quantization to images using custom color schemes, such as grayscale or sepia, to create stylized versions of the images.

5.  **Optimize Performance for Large Images**: Implement optimizations for processing large images, such as parallel processing or memory management techniques.

6.  **Create a User Interface for Quantization**: Develop a simple user interface that allows users to select images and adjust quantization settings, enhancing the interactivity of the process.

7.  **Generate Artistic Patterns**: Use quantized images to generate artistic patterns or mosaics, experimenting with the visual possibilities of reduced color palettes.

8.  **Quantization for Animated GIFs**: Extend the quantization process to handle animated GIFs, maintaining consistency in the color palette across frames.

9.  **Compare Quantization Algorithms**: Implement and compare different quantization algorithms, such as median cut or octree quantization, analyzing their strengths and weaknesses.

10.  **Profile and Analyze Algorithm Performance**: Use profiling tools to analyze the performance of the quantization algorithms and identify areas for optimization.

* * *

## Exchange Colors

**Source code**: `21_exchange_colors.cpp`

![Original Image](resources/20_colorquantizer_quantized.jpg)

Figure 85\. Original Image

![Blue exchanged with green](resources/21_exchangecolors.jpg)

Figure 86\. Blue exchanged with green

### Introduction

Manipulating colors in images is a common task in graphics programming. This chapter explores how to exchange colors in an image using C++ programming, focusing on a specific case where certain colors are targeted for alteration. This technique is instrumental in color correction, artistic filtering, and data visualization tasks.

### The Concept of Color Exchange

Color exchange involves identifying specific colors in an image and replacing them with different colors. This process can significantly change the look of an image or highlight certain aspects. In our case, we focus on exchanging blue hues with another color, which demonstrates the basic principles of color manipulation.

### Implementing Color Exchange in C++

In the implementation, we developed the `ExchangeColors` class that handles the process of reading an image, identifying specific colors, and performing the color exchange. The class uses a palette-based approach, where each color in the image is represented as an index in a color palette.

### Reading the Color Palette and Image Data

The first step in color exchange is to read the color palette and the indexed image data. The `readPalette` method reads the palette from a text file, and the `readIndexedImage` method reads the image data, which is stored as indices corresponding to the colors in the palette. We discuss how to handle file operations and data parsing in C++.

### Identifying and Exchanging Colors

The core of the color exchange process is identifying specific colors in the palette and exchanging them with new ones. In our example, we target blue hues, identifying them based on their RGB values and then swapping the green and blue components to create a new color. This showcases how to manipulate RGB values and apply conditional logic in C++.

### Generating and Writing the Modified Image

After exchanging the colors in the palette, we generate a new image using the modified palette and the original image data. The `generateImage` method creates the new image, and the `writePPMP6` method writes it to a file in the PPM format. This section covers image generation and file writing techniques in C++.

### Practical Application: Color-Correcting an Image

We apply the color exchange technique to color-correct an image, altering its appearance by targeting specific colors. This practical example illustrates the real-world application of color exchange and its impact on the visual quality of images.

### Challenges and Solutions in Color Exchange

Color exchange can be challenging, especially when dealing with many colors or complex images. We address these challenges by discussing efficient ways to process color data and strategies for accurately identifying colors to be exchanged.

### Advanced Techniques: Customizing the Color Exchange Process

Beyond basic color exchange, we explore how to customize the process for different applications. This includes adjusting the criteria for color identification, experimenting with different color replacement strategies, and extending the technique to handle more complex color transformations.

### About the code

The `21_exchange_colors.cpp` program is designed to exchange blue colors with green in a given image. It explicitly targets images that have been color quantized, typically involving a reduced palette and an indexed image representation. This program is an excellent example of manipulating color palettes in images to achieve specific color transformations.

In this program, a `Color` struct is defined to hold red, green, and blue values as `uint8_t,` representing the standard 8-bit per channel color depth in most images. The `ExchangeColors` class encapsulates the functionality of the program.

The constructor of `ExchangeColors` takes a filename as an argument and initiates a series of function calls to read the color palette and indexed image, exchange the colors, and finally write the modified image.

The `readPalette` function opens and reads the color palette from a text file. This file, created by a color quantizer program, contains the palette used to represent the quantized image. The program reads each color, and if it is predominantly blue (determined by the `isBlue` function), it exchanges that color’s green and blue components. This effectively turns what was originally blue in the image into green.

The `readIndexedImage` function reads the indexed image file, representing the original image with colors indexed from the palette. Each pixel in the indexed image is stored as an index in the palette array.

After reading the palette and indexed image, the `generateImage` function reconstructs the image using the modified palette. It creates a vector of `Color` structs, each representing a pixel in the image, by mapping each index in the indexed image to its corresponding color in the palette.

Finally, the `writePPMP6` function writes the modified image to a PPM file. The PPM (Portable Pixmap) format is a simple, uncompressed image format, and the program writes the image in the P6 (binary) format. This step involves iterating over the reconstructed image vector and writing each pixel’s RGB values to the file.

### Conclusion

Color exchange is an essential technique in graphics programming, offering a powerful tool for image manipulation. Through this chapter, programmers learn the technical aspects of color exchange in C++ and gain insights into the broader context of color manipulation in digital images. The skills and knowledge acquired here are invaluable for anyone interested in image processing, computer graphics, or data visualization.

### Exercises

To enhance your understanding and skills in color exchange with C++, consider the following exercises:

1.  **Experiment with Different Color Transformations**: Try replacing different colors or groups of colors and observe the effects on various images.

2.  **Implement a User Interface for Color Selection**: Create a simple user interface that allows users to select colors for exchange, enhancing the interactivity of the process.

3.  **Optimize for Large Images**: Implement optimizations for processing large images, such as parallel processing or efficient data structures.

4.  **Create Artistic Filters**: Use the color exchange technique to create artistic filters, such as sepia or grayscale, and apply them to images.

5.  **Analyze Color Distribution**: Before performing a color exchange, analyze the color distribution in the image to make informed decisions about which colors to target.

6.  **Extend to Animated Images**: Adapt the color exchange process to handle animated images, ensuring consistent color transformation across frames.

7.  **Interactive Color Correction**: Implement an interactive tool where users can adjust the color exchange parameters and see real-time updates on the image.

8.  **Color Exchange Based on Image Content**: Integrate image analysis to perform color exchange based on the image’s content, such as targeting specific objects or regions.

9.  **Profile and Optimize Algorithm Performance**: Use profiling tools to analyze the performance of your color exchange algorithm and identify areas for optimization.

10.  **Compare with Professional Tools**: Compare your color exchange results with those from professional image editing tools and analyze the differences.

* * *

## Sprite Animation Tester

**Source code**: `22_sprite_animation_tester.cpp`

**Note**: Uses Zlib for compression and crc32 calculations in APNG.

![Battle Squadron - Overworld Enemies Sprite Sheet](resources/output_Overworld_Enemies_montage.jpg)

Figure 87\. Battle Squadron - Overworld Enemies Sprite Sheet

### Introduction

Sprite animations bring characters and scenes to life in game development and graphical applications. This chapter delves into creating sprite animations using C++, focusing on constructing an animated PNG (APNG) file that showcases a series of sprite images.

### Understanding Sprite Animations

Sprite animations display a sequence of images, or frames, to create the illusion of motion. Each frame is a static image; when these images are shown rapidly, they create an animated effect. In our implementation, we use APNG, an extension of the PNG format that supports animations.

### Implementing Sprite Animation in C++

To create a sprite animation, we developed a class `APNG` that manages the creation of an APNG file. This class includes functionalities for writing the necessary PNG chunks, handling file operations, and compressing image data. The implementation demonstrates file handling, binary data manipulation, and image processing in C++.

### Reading and Preparing Frames

The initial step in creating a sprite animation is to read individual sprite images (frames) and prepare them for inclusion in the APNG file. The `readPPMP6` function reads images in the PPM format, adding filter bytes as required by the PNG specification. We discuss image file reading and data preparation techniques in C++.

### Writing the APNG File

After preparing the frames, the `APNG` class writes the APNG file. This involves writing an IHDR chunk for image metadata, an acTL chunk for animation control, fcTL chunks for frame control, and IDAT/fdAT chunks for image data. We explore constructing and writing these chunks to create a valid APNG file.

### Creating the Animation Sequence

We sequence the frames using the `APNG` class to create the animation. Each frame is added to the APNG file with specified timing information, controlling how long each frame is displayed. This section covers how to sequence frames effectively to create smooth animations.

### Practical Application: Testing Sprite Animations

We apply these concepts to test sprite animations, creating an APNG file from several sprite images. This practical example is a testing tool for sprite animations, allowing developers to preview and refine their animations.

### Challenges and Solutions in Sprite Animation

Creating sprite animations in C++ presents challenges like managing large numbers of frames, optimizing file size, and ensuring smooth playback. We address these challenges with efficient data handling techniques and best practices in animation design.

### Advanced Techniques: Enhancing Sprite Animations

Moving beyond basic animations, we explore advanced techniques to enhance sprite animations. This includes adding transitions between frames, experimenting with different frame rates, and implementing looping and other playback controls.

### About the code

In `22_sprite_animation_tester.cpp,` the code demonstrates creating an animated PNG (APNG) file from a series of individual PPM images, using zlib for compression and CRC32 calculations. This process demonstrates the creation of sprite animations commonly used in video games and other graphical applications.

The program starts by defining the `APNG` class, which encapsulates the functionality needed to create an animated PNG file. The class contains private member variables to store information about the APNG file, like filename, dimensions, number of frames, frame delay, and options for frame disposal and blending.

The `deflate` function within the `APNG` class compresses raw image data using zlib’s `compress2` function. This is important because PNG and APNG files are typically compressed to reduce file size.

The `crc32Calculation` function computes the CRC (Cyclic Redundancy Check) for each chunk of data in the PNG file. This is a checksum used to ensure data integrity in PNG files.

The `write_chunk` function writes individual chunks of the PNG file. A PNG file consists of several chunks of data, each serving a different purpose (like the IHDR chunk for basic image information, IDAT for image data, etc.). This function writes each chunk’s length, type, data, and CRC.

The `write_idat` function is used to write the IDAT chunk, which contains the actual image data for the first frame of the animation. The `fdAT` chunks are used for subsequent frames, which are handled in the `write_frame` function.

The `write_ihdr,` `write_actl,` and `write_fcTL` functions write the IHDR, acTL (animation control), and fcTL (frame control) chunks, respectively. The IHDR chunk contains basic information about the image, acTL specifies the number of frames and loops for the animation, and fcTL provides information specific to each frame, like delay time and disposal method.

In the `main` function, the program reads a series of PPM images (representing animation frames), converts them to a format suitable for APNG, and uses the `APNG` class to create the animated PNG file. The `readPPMP6` function reads each frame from a PPM file and prepares it for inclusion in the APNG.

Each frame’s data is added to the APNG file with appropriate compression and chunk formatting. The program iterates over all the frames, adding each to the APNG file. Finally, the `close` method of the `APNG` class is called to finish writing the file and close it properly.

This code effectively demonstrates creating an animated image file format from individual frames, highlighting compression, chunk-based file structure, and CRC calculations. These are all essential aspects of working with advanced image file formats in graphics programming.

### Conclusion

Sprite animation is a critical element of game development and graphical programming. This chapter provides a comprehensive guide to creating sprite animations in C++, from reading individual frames to constructing a complete animated sequence. The skills and insights gained here are invaluable for anyone interested in game development, animation, or graphical programming with C++.

### Exercises

To enhance your understanding and skills in sprite animation with C++, consider the following exercises:

1.  **Experiment with Different Frame Rates**: Try creating animations with different frame rates and observe how it affects the smoothness and perception of motion.

2.  **Implement Custom Animation Controls**: Add features like pausing, reversing, or changing the speed of the animation during playback.

3.  **Optimize for a Large Number of Frames**: Implement optimizations for handling animations with many frames, such as efficient memory management or image compression techniques.

4.  **Create Composite Animations**: Combine multiple sprite animations into a single APNG file, coordinating the animations to work together.

5.  **Add Transition Effects Between Frames**: Implement transition effects between frames, such as fading or sliding, to create more complex animations.

6.  **Interactive Sprite Animation Tester**: Develop a user interface that allows users to load sprite images, set animation parameters, and preview the animation.

7.  **Profile and Optimize Animation Performance**: Use profiling tools to analyze your animation’s performance and identify improvement areas.

8.  **Create Animations with User-Generated Content**: Allow users to upload or create their sprites and generate animations from them.

9.  **Automate Animation Creation from a Sprite Sheet**: Develop a tool that automatically creates animations from a sprite sheet, identifying and extracting individual frames.

10.  **Compare with Professional Animation Tools**: Compare your sprite animations with those created using professional animation software and analyze the differences in quality and functionality.

* * *

## PPM Compressor

**Source code**: `22_PPM_compressor.cpp`

**Note**: Uses ZLib for compression, decompression and crc32 calculation.

### Introduction

Compression is fundamental in computer graphics and image processing, especially for large image files like those in the PPM (Portable Pixmap) format. This chapter explores creating a compressor and decompressor for PPM files using C++, focusing on implementing compression algorithms and file-handling techniques.

### Understanding Image Compression

Image compression involves reducing the size of an image file without significantly affecting its quality. This process is crucial for efficient storage and transmission of images. In our implementation, we use zlib, a software library for data compression, to compress and decompress PPM image files.

### Implementing PPM Compression in C++

To handle PPM compression, we developed the `CPPM` class. This class manages the reading of PPM files, compresses the image data using zlib, and writes the compressed data to a new file with a custom file extension (`.cppm).` We discuss the integration of external libraries (zlib) and the handling of binary data in C++.

### Reading PPM Files

The first step in the compression process is to read the original PPM file. The `readFileToVector` method reads the file into a `std::vector<uint8_t>,` which stores the image data as a sequence of bytes. We cover efficient file reading strategies and error handling in C++.

### Compressing and Writing the Data

After reading the image data, the `deflate` method compresses it using Zlib’s compression functionalities. The compressed data is then written to a new file with the `.cppm` extension using the `writeVectorToFile` method. This section highlights the use of zlib for compression and the writing of binary data to files.

### Decompressing CPPM Files

In addition to compression, our class handles the decompression of `.cppm` files back to the original PPM format. The `inflate` method decompresses the data, and the decompressed image is written to a PPM file. We discuss decompression techniques and the reversal of the compression process.

### Practical Application: Compressing and Decompressing Images

We apply these concepts to compress and decompress PPM image files, demonstrating the practical use of the `CPPM` class. This example serves as a helpful tool for reducing the storage requirements of PPM images and illustrates the effectiveness of compression algorithms.

### Challenges and Solutions in Image Compression

Image compression can present challenges, such as balancing compression ratio and image quality, handling large images efficiently, and ensuring compatibility with different image formats. We address these challenges with strategies for optimizing compression and ensuring data integrity.

### Advanced Techniques: Custom Compression Algorithms

Beyond standard Zlib compression, we explore the possibility of implementing custom compression algorithms tailored for specific types of images or applications. This includes lossy compression techniques and specialized algorithms for specific image characteristics.

### About the code

The `22_PPM_compressor.cpp` program is designed to compress and decompress PPM (Portable Pixmap) image files, saving them in a custom CPPM format. This is achieved using ZLib, a widely-used library for data compression, which provides functions for compression (deflation) and decompression (inflation) as well as for CRC32 (Cyclic Redundancy Check) calculations. The CPPM format is intended to save space on disk or in RAM, particularly useful for large images or when managing a collection of images.

The core of this program lies in the `CPPM` class. This class handles the reading of PPM files, compresses them to CPPM format, decompresses CPPM files back to PPM, and writes the resulting images back to disk. It uses two main vectors, `input` and `output,` to store the image data during processing.

The `crc32Calculation` function calculates the CRC32 checksum of the given data. This checksum is crucial for verifying the integrity of the data during decompression.

The `deflate` function compresses the input data using zlib’s `compress2` function with the best compression setting, `Z_BEST_COMPRESSION.` It returns the size of the compressed data. In contrast, the `inflate` function decompresses the data. It attempts to uncompress the data in a loop, increasing the buffer size until successful or until a maximum attempt limit is reached.

File operations are performed by `readFileToVector` and `writeVectorToFile.` The former reads a file into the `input` vector, while the latter writes the contents of the `output` vector to a file.

Metadata handling is done by the `concatenateData` and `extractDataFromVector` functions. `concatenateData` appends metadata (like file size and CRC checksum) to the compressed data, and `extractDataFromVector` does the reverse, extracting metadata from the input vector and preparing the data for decompression.

The class constructor handles the workflow. It opens the input file, determines if it needs to compress or decompress based on the file suffix (`.ppm` for PPM, `.cppm` for CPPM), and performs the necessary operations. If the file is a PPM, it compresses it to CPPM format. If it’s a CPPM, it decompresses it back to PPM.

The program accepts command-line arguments for the input and optional output file names in the’ main’ function. Depending on the number of arguments provided, it either compresses or decompresses the specified file.

Overall, this program showcases a practical application of data compression in handling image files. Converting PPM files to a compressed format demonstrates using Zlib effectively for such tasks. This is especially useful in applications where managing large sets of images efficiently is crucial.

### Conclusion

Image compression is an essential skill in computer graphics and image processing. This chapter provides a detailed guide to implementing PPM compression and decompression in C++, from reading image files to applying compression algorithms and handling binary data. The knowledge and experience gained here are invaluable for anyone interested in image file handling and data compression in C++.

### Exercises

To enhance your understanding and skills in image compression with C++, consider the following exercises:

1.  **Implement Lossy Compression**: Explore implementing a simple lossy compression algorithm and compare its performance with Zlib’s lossless compression.

2.  **Optimize for Large Images**: Implement optimizations for handling large image files, such as memory management techniques or parallel processing.

3.  **Develop a Compression Quality Evaluator**: Create a tool that evaluates the quality of compressed images, comparing them with the original images.

4.  **Support Additional Image Formats**: Extend the `CPPM` class to handle additional image formats, such as JPEG or PNG.

5.  **Create a Batch Compression Tool**: Implement functionality to compress multiple images in a batch process, improving efficiency for large numbers of images.

6.  **Visualize Compression Effects**: Develop a visualization tool that shows the differences between the original and compressed images, highlighting areas of significant change.

7.  **Compare with Standard Image Compression Tools**: Compare the performance of your compression tool with standard image compression software, analyzing differences in compression ratio and speed.

8.  **Add a standard library implementation of ZLib features**: Make the code complete with adding compression, decompression, crc32 calculation with standard library.

* * *

## Anti-Aliasing

**Source code**: `23_anti_aliasing.cpp (and ppmpp.hpp)`

![Original Image](resources/23_original.jpg)

Figure 88\. Original Image

![Anti-Aliased](resources/23_anti_aliasing.jpg)

Figure 89\. Anti-Aliased

### Introduction

Anti-aliasing is a crucial technique in computer graphics that reduces visual defects when high-resolution images are represented on lower-resolution displays. This chapter focuses on implementing anti-aliasing in C++, specifically enhancing image line and curve rendering.

### Understanding Anti-Aliasing

Anti-aliasing smooths out jagged edges, known as `aliasing,` in digital images. This is particularly noticeable in diagonal lines or curves. By applying anti-aliasing, we can improve the visual quality of images, making them appear smoother and more natural.

### Implementing Anti-Aliasing in C++

Implementing anti-aliasing in our C++ program involves manipulating pixel data to create a smoother transition between edges and the background. We use the `ppmpp` library, which provides functionalities for image manipulation, including drawing lines and Bezier curves and applying anti-aliasing.

### Drawing Lines and Curves

Before applying anti-aliasing, we first draw lines and Bezier curves on an image. The `drawLine` and `drawBezierCubic` methods from the `ppmpp` library are used. We discuss the mathematical principles behind these methods and how to plot lines and curves accurately on a pixel grid.

### Applying Anti-Aliasing

After drawing lines and curves, we apply anti-aliasing to the image. The `applyAntiAliasing` method smooths out jagged edges by blending the colors of edge pixels with their surrounding pixels. This section explains how to calculate the intensity of pixel colors and blend them to achieve the anti-aliasing effect.

### Practical Application: Enhancing Image Quality

We apply these concepts to enhance the quality of a digital image, focusing on smoothing the edges of lines and curves. This practical example demonstrates the effectiveness of anti-aliasing in improving the visual appeal of graphics rendered in C++.

### Challenges and Solutions in Anti-Aliasing

Implementing anti-aliasing presents challenges, such as determining the appropriate level of pixel blending and managing its impact on image processing performance. We explore solutions to these challenges, emphasizing efficient algorithms and optimization techniques in C++.

### Advanced Techniques: Adaptive Anti-Aliasing

Moving beyond basic anti-aliasing, we explore adaptive anti-aliasing techniques that apply varying levels of smoothing based on the specific needs of different image regions. This includes analyzing image content to apply more intensive anti-aliasing where needed.

### About the code

The `23_anti_aliasing.cpp` program demonstrates anti-aliasing in 2D graphics to create smoother images, particularly when rendering curves and lines. It employs the `ppmpp.hpp` graphics library, which provides drawing and image manipulation functions.

The program starts by defining a type alias, `BezierControlPoints,` for a tuple of four `ppm::Point` objects. These points will represent the control points for Bezier curves. Bezier curves are commonly used in computer graphics to model smooth curves and are defined by a set of control points.

The `main` function begins by creating a vector of `BezierControlPoints.` These are then populated with data representing various curves. The data for these curves is obtained from a series of strings, each containing eight integer values. These values are parsed using a `std::istringstream` and represent the x and y coordinates of the four control points for each Bezier curve. An offset is applied to these points to position them correctly within the image.

Additionally, the program sets up a list of coordinates for straight lines using `ppm::Coord` objects. These lines are also part of the image being drawn.

Next, the program creates an image object `img` with specified dimensions and sets all its pixels to a dark color. This color serves as the background for the drawing.

The program then iterates over the Bezier curve control points and draws each curve on the image using the `drawBezierCubic` function provided by the `ppmpp.hpp` library. This function takes four control points and draws a cubic Bezier curve. A similar process is followed for the lines, using the `drawLine` function to render each line specified in the `lineData.`

The program’s key feature is the application of anti-aliasing, which is done through the `applyAntiAliasing` function. Anti-aliasing is used in computer graphics to minimize the jagged edges in digital images, especially around curves and diagonal lines. This is achieved by smoothing out the color transitions between the edges of the lines and the background.

Finally, the program writes the resulting image to a file named `23_anti_aliasing.ppm.` The output is an image where the drawn Bezier curves and lines appear smoother and more visually appealing, demonstrating the effectiveness of anti-aliasing in enhancing the quality of digital graphics. This example is handy for readers looking to understand how to implement and see the effects of anti-aliasing in image processing and computer graphics.

### Conclusion

Anti-aliasing is an essential technique in computer graphics for producing high-quality images. This chapter provides a comprehensive guide to implementing anti-aliasing in C++, from basic line and curve rendering to advanced pixel manipulation techniques. The skills and knowledge acquired here are invaluable for anyone interested in graphics programming and image processing.

### Exercises

To enhance your understanding and skills in anti-aliasing with C++, consider the following exercises:

1.  **Experiment with Different Anti-Aliasing Intensities**: Try applying different levels of anti-aliasing to images and observe the effects on image quality and processing time.

2.  **Implement Multisample Anti-Aliasing (MSAA)**: Explore implementing MSAA, a technique that samples multiple points within each pixel and averages the results to smooth out edges.

3.  **Optimize Anti-Aliasing Performance**: Implement optimizations for anti-aliasing algorithms, focusing on reducing processing time without compromising image quality.

4.  **Develop a User Interface for Anti-Aliasing Settings**: Create a simple user interface that allows users to adjust anti-aliasing settings and see the results in real time.

5.  **Apply Anti-Aliasing to Text Rendering**: Extend the anti-aliasing technique to smooth the edges of text rendered in images, improving readability and visual appeal.

6.  **Compare Anti-Aliasing Techniques**: Implement and compare different anti-aliasing techniques, such as supersampling and post-processing filters, analyzing their strengths and weaknesses.

7.  **Profile and Optimize Algorithm Performance**: Use profiling tools to analyze the performance of your anti-aliasing algorithm and identify areas for optimization.

8.  **Integrate Anti-Aliasing with Other Image Processing Techniques**: Combine anti-aliasing with other image processing techniques, such as color correction or sharpening, to enhance overall image quality.

9.  **Automate Anti-Aliasing Level Based on Image Content**: Develop an algorithm that automatically adjusts the anti-aliasing level based on the image’s content, such as applying more anti-aliasing to areas with more curves or diagonal lines.

* * *

## Bloom Effect

**Source code**: `24_bloom.cpp` (and ppmpp.hpp)

![Original Image](resources/23_anti_aliasing.jpg)

Figure 90\. Original Image

![With Bloom Effect](resources/24_bloom.jpg)

Figure 91\. With Bloom Effect

### Introduction

The bloom effect is a popular post-processing technique in computer graphics, often used to simulate an extremely bright light bleeding into surrounding areas. This chapter focuses on implementing the bloom effect in C++ using the `ppmpp` library, enhancing the visual appeal of images by mimicking the way the human eye perceives bright light.

### Understanding the Bloom Effect

The bloom effect creates a realistic representation of how very bright light affects the human eye, producing a halo-like glow around light sources. In digital images, this effect adds depth and atmosphere, making bright areas of the image stand out and feel more dynamic.

### Implementing Bloom in C++

We implement the bloom effect using the `ppmpp` library, which provides comprehensive functionalities for image processing. The `applyBloom` method in the `Image` class applies the bloom effect to an image. We discuss how to determine the bloom’s intensity, the glow’s spread, and how to blend it with the original image.

### Algorithm for Bloom Effect

The bloom effect algorithm identifies bright areas of the image and applies a Gaussian blur to these areas to create the halo effect. The blurred image is then combined with the original image, adjusting the intensity of the bloom to achieve the desired effect. We explore Gaussian blur algorithms and techniques for selectively applying blur to parts of an image.

### Practical Application: Enhancing Images with Bloom

We apply the bloom effect to a digital image, focusing on enhancing bright areas and creating a more visually appealing image. This practical example demonstrates the utility of the bloom effect in graphics programming and how it can be used to improve the realism and aesthetic quality of images.

### Challenges and Solutions in Bloom Effect Implementation

Implementing the bloom effect in C++ can be challenging, mainly when dealing with performance optimization and accurately determining which areas of the image should receive the effect. We discuss solutions to these challenges, including efficient image processing techniques and adaptive algorithms for identifying bright areas.

### Advanced Techniques: Customizing the Bloom Effect

Beyond basic implementation, we explore ways to customize the bloom effect. This includes adjusting the size and intensity of the bloom, applying the effect to specific color channels, and combining the bloom effect with other image processing techniques for more complex visual results.

### About the code

The `24_bloom.cpp` program is a concise yet effective demonstration of applying a bloom effect to an image using the `ppmpp.hpp` graphics library. Bloom is a popular image processing effect used in computer graphics to simulate an extremely bright light overwhelming the camera capturing the scene. It creates a visually pleasing soft glow around bright areas of an image.

The program begins by loading an image from a file. Here, the image being processed is `23_anti_aliasing.ppm,` presumably an image generated from a previous program (as the name suggests, possibly one that has applied anti-aliasing techniques). The `ppm::Image` class, provided by the `ppmpp.hpp` library, handles image loading, manipulation, and saving.

The following line in the program is where the bloom effect is applied to the image. The `applyBloom` function of the `ppm::Image` class is called with two parameters: a threshold and a radius. The threshold (0.1 in this case) determines the minimum brightness level of pixels that will contribute to the bloom. Only pixels brighter than this threshold will be affected. The radius (25.0 in this example) specifies the extent of the bloom effect around the bright areas. A larger radius results in a more pronounced bloom.

After applying the bloom effect, the modified image is saved to a new file, `24_bloom.ppm.` This file contains the original image with the added bloom effect, which typically enhances the visual appeal, especially for scenes with light sources or reflections.

This simple yet powerful example shows how a high-level graphics library can be used with minimal code to implement advanced graphical effects like Bloom. Such effects are widely used in various domains of computer graphics, including video games, simulations, and artistic digital renderings, to enhance realism or create a specific atmosphere in an image.

### Conclusion

The bloom effect is a powerful tool in the arsenal of a graphics programmer, adding a layer of realism and depth to digital images. This chapter provides a detailed guide to implementing the bloom effect in C++, from understanding the underlying principles to practical application in image enhancement. The skills and insights gained here are valuable for anyone interested in advanced image processing and computer graphics.

### Exercises

To enhance your understanding and skills in implementing the bloom effect with C++, consider the following exercises:

1.  **Experiment with Different Bloom Intensities**: Try applying the bloom effect with varying intensities and observe the effects on different types of images.

2.  **Implement Multi-color Bloom**: Extend the bloom effect to apply different colors to the bloom based on the color of the light source in the image.

3.  **Optimize Bloom Algorithm Performance**: Implement optimizations for the Bloom algorithm, focusing on reducing processing time without compromising image quality.

4.  **Develop a User Interface for Bloom Settings**: Create a simple user interface that allows users to adjust Bloom settings and see the results in real-time.

5.  **Apply Bloom to Animated Images**: Adapt the bloom effect to handle animated images, ensuring consistent effect application across frames.

6.  **Combine Bloom with Other Effects**: Combine the bloom effect with other image processing techniques, such as lens flares or color grading.

7.  **Profile and Optimize Algorithm Performance**: Use profiling tools to analyze your bloom algorithm’s performance and identify improvement areas.

8.  **Create Customizable Bloom Filters**: Develop a tool that allows for customizable bloom filters, giving users control over the shape and spread of the bloom.

9.  **Adaptive Bloom Based on Image Content**: Implement an algorithm that adjusts the intensity and size of the bloom effect based on the image’s content, such as applying more intense bloom to brighter areas.

* * *

## Lens Effect

**Source code**: `25_lens.cpp` (and ppmpp.hpp)

![Original Image](resources/28_input.jpg)

Figure 92\. Original Image

![With Lens Effect](resources/25_lens.jpg)

Figure 93\. With Lens Effect

### Introduction

In computer graphics, simulating optical effects such as lens distortions can significantly enhance images’ realism and artistic appeal. This chapter focuses on implementing a lens effect in C++ using the `ppmpp` library, which enables us to simulate the visual impact of viewing an image through a lens.

### Understanding the Lens Effect

A lens effect in digital imaging simulates the distortion seen when viewing objects through a curved lens. This can include effects like magnification, light bending, and edge blurring. In our implementation, we aim to create a lens effect that enhances the image’s visual appeal by introducing a sense of depth and curvature.

### Implementing Lens Effect in C++

The lens effect is implemented through the `applyLens` method in the `Image` class of the `ppmpp` library. This method alters the pixels of an image to simulate the effect of viewing them through a lens. We discuss the mathematical basis for lens distortion and how to apply it to pixel data.

### Algorithm for Lens Effect

The algorithm for the lens effect involves calculating the displacement of each pixel in the image to simulate the curvature of a lens. This displacement depends on factors like the distance from the center of the image (or the lens) and the intensity of the lens effect. We explore creating a visually pleasing lens effect that can be adjusted for different intensities and styles.

### Practical Application: Enhancing Images with Lens Effect

We apply the lens effect to a digital image to demonstrate its impact. The practical example shows how the lens effect can draw attention to specific areas of an image or create artistic distortions that enhance the overall composition.

### Challenges and Solutions in Lens Effect Implementation

Implementing the lens effect in C++ can present challenges, especially regarding performance optimization and achieving a realistic distortion. We discuss solutions to these challenges, including techniques for efficient pixel manipulation and strategies for achieving more natural-looking distortions.

### Advanced Techniques: Customizing the Lens Effect

Beyond basic implementation, we explore ways to customize the lens effect. This includes creating different lens distortions (such as fisheye or concave effects), adjusting the area of effect, and combining the lens effect with other image processing techniques for more complex results.

### About the code

The program `25_lens.cpp` is designed to apply a lens effect to an image, enhancing it with a distinctive visual distortion that simulates the effect of viewing the scene through a lens. This is achieved using the `ppmpp.hpp` graphics library, which provides tools for image manipulation in 2D graphics programming.

The process begins with loading an image file into the `ppm::Image` object. In this case, the image loaded is `28_input.ppm.` This file is an existing image that will be the subject of the lens effect. The `ppm::Image` class from the `ppmpp.hpp` library offers functionalities like loading, modifying, and saving image files, which are crucial for image processing tasks.

Once the image is loaded into the program, the following essential step is to apply the lens effect. This is done using the `applyLens` function on the `img` object. The `applyLens` function takes an integer parameter that controls the intensity or strength of the lens effect. In this program, the value provided is `8,` which determines how pronounced the lens effect will be. The lens effect typically creates a visual distortion where parts of the image appear magnified or warped, simulating the effect of passing the scene through a convex or concave lens.

After applying the lens effect, the altered image is saved to a new file. The `write` method of the `ppm::Image` class is used for this purpose, and the output file is named `25_lens.ppm.` This file contains the original image now altered with the lens effect, which can add a unique and artistic touch to the image, often used in graphic design, photography, and computer graphics to create a sense of depth or to draw attention to specific parts of the image.

The program exemplifies how a high-level graphics library like `ppmpp.hpp` can implement complex image effects such as lens distortion. These effects are widely used in digital art and photography, video game graphics, and in simulating optical phenomena for educational or entertainment purposes.

### Conclusion

The lens effect is a powerful tool in graphics programming, adding depth and interest to digital images. This chapter provides a comprehensive guide to implementing the lens effect in C++, covering everything from basic pixel manipulation to creating sophisticated optical distortions. The skills and insights gained here are valuable for anyone interested in image processing and computer graphics.

### Exercises

To enhance your understanding and skills in implementing the lens effect with C++, consider the following exercises:

1.  **Experiment with Different Lens Intensities**: Try applying the lens effect with varying intensities and observe the effects on different types of images.

2.  **Implement Various Lens Types**: Extend the lens effect to simulate different types of lenses, such as convex, concave, or fisheye lenses.

3.  **Optimize Lens Algorithm Performance**: Implement optimizations for the lens algorithm, focusing on reducing processing time without compromising image quality.

4.  **Develop a User Interface for Lens Settings**: Create a simple user interface that allows users to adjust lens settings and see the results in real time.

5.  **Apply Lens Effect to Animated Images**: Adapt the lens effect to handle animated images, ensuring consistent effect application across frames.

6.  **Combine Lens with Other Effects**: Combine the lens effect with other image processing techniques, such as bloom or color grading.

7.  **Profile and Optimize Algorithm Performance**: Use profiling tools to analyze your lens algorithm’s performance and identify improvement areas.

8.  **Create Customizable Lens Filters**: Develop a tool that allows for customizable lens filters, giving users control over the shape and intensity of the lens effect.

9.  **Adaptive Lens Based on Image Content**: Implement an algorithm that adjusts the intensity and area of the lens effect based on the image’s content, such as applying stronger effects to brighter areas.

* * *

## Easing Animation

**Source code**: `26_easing_animation.cpp`

**Note**: Uses ZLib for APNG

### Introduction

The art of animation in programming transcends mere movement; it embodies the essence of bringing vitality to graphics. Easing animations, in particular, play a pivotal role in rendering more lifelike movements. This chapter delves into the implementation of easing functions in C++ programming, a journey that enhances the expressiveness of our graphical endeavors.

### The Role of Easing in Animation

Animations are critical to modern interfaces and games, contributing significantly to user experience. Easing functions modify the rate of change over time, transitioning from linear to more dynamic movements. In C++, easing can be leveraged to create animations that mimic the subtleties of real-world motion, providing a more natural and engaging user interaction.

### Understanding Easing Functions

Easing functions determine how graphical elements move within a given timeframe. They are categorized into three primary types: ease-in, ease-out, and ease-in-out. Each type offers a unique motion characteristic: ease-in functions start slowly and accelerate, ease-out parts begin quickly and decelerate, and ease-in-out functions combine both for a smooth start and finish. C++ programmers can use these to create animations that feel more organic and less mechanical.

### Implementing Easing in C++

In C++, we implement easing functions within a dedicated class, encapsulating various easing behaviors. Utilizing the C++ Standard Library, we can employ mathematical functions like `std::sin,` `std::cos,` `std::pow,` and `std::sqrt` to perform the necessary easing calculations. These functions return a value representing the position of an animated object at a specific point in time based on the chosen easing function.

### Easing Functions in Depth

We explore several easing functions, each with its mathematical formula and characteristic motion:

1.  **Linear Easing**: The simplest form, providing uniform motion.
2.  **Quadratic Easing**: Introduces acceleration, giving a sense of speed-up.
3.  **Cubic and Quartic Easing**: Offers more pronounced acceleration curves.
4.  **Elastic and Bounce Easing**: Mimics elastic and bouncing motions, adding playful dynamics to animations.

Each easing function provides a distinct aesthetic and feel, allowing C++ programmers to tailor animations to the specific needs of their application.

### Practical Application: Animating with Easing

We create a simple animation to demonstrate these concepts: a moving circle in a graphical window. This practical example uses a combination of the C++ Standard Library and a basic graphics library to render and animate a circle using various easing functions. We iterate over a set number of frames, calculating the circle’s position using our easing functions for each frame, resulting in a smooth, dynamic animation.

### Challenges and Solutions in Easing Animations

Implementing easing animations in C++ has its challenges. Balancing performance and visual fidelity, especially in resource-intensive applications like games or interactive simulations, is crucial. To address these challenges, we discuss optimization techniques such as pre-calculating easing values and leveraging C++’s advanced features like smart pointers and templates for efficient memory and resource management.

### Beyond Basics: Advanced Easing Techniques

As we advance our skills in C++ programming, we can explore more complex easing scenarios. This includes chaining multiple easing functions for complex animations, combining easing with other animation techniques like keyframe animation, and creating custom easing functions to achieve specific animation effects.

### About the code

The `26_easing_animation.cpp` program is an example of creating a simple animated effect using easing functions and the APNG (Animated Portable Network Graphics) format. The animation portrays a bouncing ball, achieved through drawing techniques and easing functions to simulate the motion’s dynamics.

Firstly, the program includes the necessary headers and libraries, including `cmath` for mathematical calculations, `vector` and `tuple` for handling data structures, `fstream` and `iostream` for file operations, `zlib.h` for compression needed in APNG creation, and `ppmpp.hpp` for image processing.

The `APNG` class is defined to handle creating an animated PNG file. It manages file writing, compressing image data using ZLib, and organizing data into the correct PNG format. It includes functions like `deflate` for compression, `crc32Calculation` for generating checksums, `write_chunk` for writing different PNG chunks (like IHDR, acTL, fcTL, IDAT, fdAT), and `close` for finalizing the file.

Next, the `Easing` class within the `ease` namespace provides various easing functions. These functions are mathematical formulas that create smooth animations by gradually changing values over time. The program uses the `easeOutBounce` function, which simulates a bouncing effect, perfect for the ball animation.

The `getRawData` function extracts the raw pixel data from an image in a format suitable for PNG creation. It iterates over the image pixels, converting them to RGB values and accounting for the PNG format’s filter byte.

In the `main` function, several constants define the animation’s properties, such as image dimensions, circle diameter, margin, and the number of frames. The loop iterates the total number of frames, creating each animation frame. For each frame, it calculates the vertical position of the ball using the `easeOutBounce` function, creating the illusion of a ball bouncing.

The `ppm::Image` object, `image,` is used to draw a white circle (representing the ball) against a black background at calculated positions for each frame. The `getRawData` function is then used to extract the raw pixel data from this image, which is written into the APNG file using the `APNG` class.

Finally, after all frames are processed, the APNG file is closed, resulting in a complete animated PNG file showcasing a bouncing ball. The program is an excellent example of combining various elements of 2D graphics programming, such as drawing shapes, creating animations, and working with image file formats to produce a visually appealing result.

### Conclusion

Easing animations are a vital tool in the C++ programmer’s toolkit, providing the means to create more natural and engaging graphical movements. Through the knowledge and examples presented in this chapter, programmers can enhance their applications with animations that are visually appealing and intuitively correct. The journey through easing in C++ programming explores how code can be transformed into art, enabling creations that resonate with users more naturally and intuitively.

### Exercises

To further enhance your understanding and skills in easing animations with C++, here are some practical exercises. These will allow you to experiment with the code and concepts discussed in the chapter:

1.  **Implement Additional Easing Functions**: Research and implement other easing functions not covered in the chapter, such as exponential, back, or bounce easing. Analyze how they differ in behavior from the standard easing functions.

2.  **Combine Multiple Easing Functions in a Single Animation**: Create an animation where different segments use different easing functions. For example, a moving object could start with an ease-in function, switch to an ease-out function, and finish with an ease-in-out function.

3.  **Create a Sequence of Animated Objects**: Animate multiple objects in a sequence, each starting its motion after the previous one has finished. Experiment with different easing functions for each object to observe the variation in motion.

4.  **Animate Different Properties**: Instead of just moving an object, try animating other properties like size, rotation, or color. Apply easing functions to these properties and observe the effects.

5.  **Create a Reversible Animation**: Design an animation that plays forwards with an easing function, then reverses back to the starting point with either the same or a different easing function.

6.  **Easing Function Visualizer**: Develop a tool that visually represents the curve of an easing function. This tool should display how the speed of an object changes over time according to the selected easing function.

7.  **Path Animation with Easing**: Instead of moving an object in a straight line, create a curved path and apply easing functions to the movement along this path.

8.  **Compare Easing Functions Side-by-Side**: Animate multiple objects side-by-side using a different easing function to compare how each function affects the motion visually.

9.  **Custom Easing Function Creation**: Try creating your own custom easing function. Experiment with different mathematical formulas to see how they affect the animation.

10.  **Easing Function Parameter Tweaking**: Play around with the parameters of standard easing functions (like modifying the exponent in a quadratic easing function) to see how it changes the animation behavior.

* * *

## Grayscale Image into Patterns

**Source code**: `27_image_to_patterns.cpp`

![](resources/27_input.jpeg)

Figure 94

![](resources/27_output.jpeg)

Figure 95

### Introduction

This chapter delves into the fascinating process of transforming grayscale images into intricate patterns using C++. It highlights the blend of artistic creativity with algorithmic precision in the realm of image processing.

### Understanding Grayscale Images and Patterns

Grayscale images, made up of shades of gray, are ideal for pattern transformations. Patterns, in this context, are pre-defined pixel arrangements representing different shades of gray. This technique illustrates how simple images can be transformed into complex visual tapestries.

### Implementing Image Transformation in C++

The heart of this transformation lies in the `27_image_to_patterns.cpp` program, which consists of several key components:

*   `GrayscalePattern` structure to store an 8x8 pattern.
*   `deserializeMetadata` function to map grayscale values to patterns.
*   `generateOutputPpm` function to apply these patterns to an image.

### The Transformation Process

1.  **Pattern Representation**: The `GrayscalePattern` struct represents an 8x8 pattern corresponding to a grayscale level.
2.  **Reading Patterns**: The `deserializeMetadata` function reads pattern data from a binary file, linking grayscale values to patterns.
3.  **Applying Patterns**: The `generateOutputPpm` function replaces each pixel in the input image with a pattern based on its grayscale value.

### Practical Application

This technique can be used in various domains, such as creating textured backgrounds in games, generating unique artworks, or enhancing data visualizations.

### Challenges in Transformation

One primary challenge is efficiently mapping pixel brightness to corresponding patterns. This is tackled through careful data mapping and algorithmic efficiency.

### Advanced Techniques

Advanced applications involve dynamic pattern generation based on image content and interactive interfaces allowing users to influence the transformation process.

### About the code

The `27_image_to_patterns.cpp` code demonstrates a sophisticated approach to 2D graphics programming in C++. It uses the `ppmpp.hpp` library for image processing and involves several functions:

*   `deserializeMetadata:` Reads and maps pattern data to grayscale values.
*   `generateOutputPpm:` Processes the input image and applies patterns to create the transformed output.

The program starts with reading a grayscale image, followed by the transformation process, resulting in an output image that is a patterned version of the original.

### Conclusion

This chapter not only teaches technical aspects of image processing with C++ but also opens avenues for artistic expression. It demonstrates the power of C++ in image manipulation, encouraging the exploration of aesthetic possibilities in computer graphics.

### Exercises

Here are some exercise suggestions for you to further explore and enhance your skills in transforming grayscale images into patterns with C++:

1.  **Custom Pattern Design**: Create your own unique patterns and integrate them into the transformation process. Experiment with different geometric shapes and sizes.

2.  **Color Extension**: Adapt the program to work with colored images, applying multicolored patterns to see how it affects the output.

3.  **Different Image Types**: Use the program with various types of images, such as nature scenes, urban landscapes, or abstract designs, to observe how the patterns interact with different image contents.

4.  **Pattern Size Variation**: Experiment with changing the size of the patterns, trying sizes larger or smaller than 8x8, and see how this impacts the visual output.

5.  **Grayscale Level Mapping Adjustment**: Modify how grayscale levels are mapped to different patterns, perhaps using a logarithmic scale or other mathematical functions for mapping.

6.  **Create Animated Transitions**: Generate a sequence of images where patterns evolve or change over time, and create an animation to visualize this transition.

7.  **Combine Multiple Patterns**: For each grayscale level, try using a combination of multiple patterns instead of a single pattern to add complexity to the output image.

8.  **Randomize Pattern Selection**: Introduce a random element in selecting patterns for each grayscale level, creating a mosaic or collage effect in the transformed image.

9.  **Automated Pattern Generation**: Write an algorithm to automatically generate unique patterns based on certain rules or mathematical formulas.

10.  **Applying Artistic Filters**: Apply various artistic filters to the transformed image, such as a vignette effect, edge enhancement, or artistic blurring, to create a more visually appealing output.

* * *

## Vintage Photo

**Source code**: `28_vintage_photo.cpp`

![](resources/28_input.jpg)

Figure 96

![](resources/28_6_output_applySepia.jpg)

Figure 97

### Introduction

This chapter explores the fascinating world of image processing by transforming modern images into vintage photos using C++. We will delve into various techniques that emulate the classic look of old photographs, including sepia tones, vignettes, and grainy textures.

### The Art of Vintage Photo Processing

Vintage photo processing involves applying a series of effects to give modern images an aged appearance. This includes color adjustments, adding noise and texture, and applying vignettes to mimic the characteristics of old photographs.

### Implementing Vintage Effects in C++

The code in `28_vintage_photo.cpp` demonstrates a sequence of image processing steps to create vintage photo effects. The main components include:

*   A `Vintage` class that encapsulates the entire process.
*   Functions to apply various effects like sepia tone, gamma correction, and vignettes.

### The Transformation Process

1.  **Read and Write the Original Image**: Load the original image and save it as a baseline for comparison.
2.  **Add Schmutz (Dirt and Scratches)**: Overlay textures to add character typical of aged photos.
3.  **Gamma Correction**: Adjust the luminance of the image to match the tone of old photographs.
4.  **Add Noise**: Introduce graininess to simulate the texture of vintage film.
5.  **Apply a Circular Vignette**: Create a vignette effect to mimic the lens and film limitations of old cameras.
6.  **Convert to Sepia Tone**: Change the image to grayscale and then apply a sepia tone for a classic vintage look.

### About the code

`28_vintage_photo.cpp` uses the `ppmpp.hpp` graphics library to manipulate images. The `Vintage` class manages the process, applying each effect in a sequence that culminates in the creation of a vintage photo. Key functions handle specific tasks like reading alpha values for textures, applying gamma correction, adding noise, and creating a vignette effect.

### Conclusion

This chapter offers an intriguing look into the world of image processing with C++. By recreating the vintage photo effect, programmers can explore a range of techniques and understand how different image processing steps contribute to the overall aesthetic of an image.

### Exercises

Here are some exercises to further your understanding and skills:

1.  **Experiment with Different Textures**: Try using various textures for the ‘schmutz’ effect to see how they change the final image.

2.  **Adjust Gamma Correction Levels**: Play with different gamma values to see how they affect the brightness and contrast of the vintage effect.

3.  **Vary the Noise Level**: Experiment with different levels of noise to find the perfect balance between realism and clarity.

4.  **Modify the Vignette Effect**: Change the parameters of the vignette effect, such as its size and opacity, to observe different styles.

5.  **Create Different Color Tones**: Besides sepia, try applying different color tones, such as cyanotype or black and white, to emulate other vintage styles.

6.  **Implement Different Aging Effects**: Explore other effects that can make a photo look aged, such as blurring, fading, or color shifts.

7.  **Create a User Interface**: Develop a simple UI to adjust the vintage effects in real-time, allowing for more interactive experimentation.

8.  **Combine with Other Image Effects**: Integrate the vintage photo processing with other image effects like blur, sharpening, or pixelation for unique results.

9.  **Automate the Process for Multiple Images**: Write a script to apply the vintage effect to a batch of images automatically.

10.  **Analyze the Effect on Different Image Types**: Apply the vintage effect to various types of images, such as portraits, landscapes, or urban scenes, to see how the effect interacts with different subjects.

These exercises are aimed at enhancing your understanding of the techniques used in transforming modern images into vintage photos using C++. Through practical application and experimentation with the code, you will gain valuable experience in various aspects of image processing, including adding texture, adjusting color tones, and applying effects like vignettes and noise to create a vintage aesthetic in C++ programming.

* * *

![](resources/ppmpp.jpg)

Figure 98

# PPMPP - Portable PixMap in C Plus Plus

## Why?

In the evolving landscape of graphics programming, efficiency and simplicity often stand at the forefront of innovation. Recognizing this need, the `ppmpp.hpp` framework emerges as a singular, streamlined solution designed for rapid generation and manipulation of graphics. Developed with a focus on ease of use, `ppmpp.hpp` encapsulates robust functionality in a single header file, allowing programmers to integrate and deploy graphic manipulations quickly. This framework is a testament to minimalist coding practices and a powerful tool for developers who require quick, effective graphic processing capabilities in their applications.

At the heart of `ppmpp.hpp` lies its compatibility with the Portable PixelMap (PPM) format, an open and widely used standard in image processing. The choice of PPM as the central file format is strategic, balancing simplicity and versatility. Unlike more complex formats that require extensive parsing and handling, PPM’s straightforward structure allows for rapid reading, writing, and manipulation of pixel data. This compatibility ensures that `ppmpp.hpp` can seamlessly integrate into various projects, enabling developers to work with a format that is both accessible and powerful.

The design philosophy behind `ppmpp.hpp` is grounded in maximizing efficiency while minimizing overhead. Every line of code in the framework is crafted to provide maximal functionality with minimal complexity, adhering to clean and maintainable code principles. This approach makes `ppmpp.hpp` a lightweight addition to any project and ensures that it remains easy to understand and modify. Whether you are a novice programmer or a seasoned developer, `ppmpp.hpp` offers an intuitive, straightforward path to powerful graphics manipulation.

As we look towards the future of graphics programming, `ppmpp.hpp` stands as a forward-thinking tool that anticipates and adapts to the field’s evolving needs. Its design is not just about solving current challenges but also about laying a foundation for future innovations. With its blend of ease of use, efficiency, and open format compatibility, `ppmpp.hpp` is more than just a framework; it is a stepping stone towards a new era in graphics programming, where power and simplicity coexist harmoniously.

At its core, it provides a range of functionalities centered around manipulating pixels and geometric shapes within images. The framework operates on a fundamental unit called `Pixel,` a tuple of three double values representing the `red,` `green,` and `blue` color channels. Additionally, it includes definitions for `Coord` and `Point,` which are tuples used for specifying coordinates and points in the image space, respectively.

Various utility functions and methods that facilitate complex image manipulations are central to the framework’s capabilities. These include functions for color manipulation (such as getRedColorElement and setGreenColorElement) and methods to create and manipulate pixels and coordinates. The `Image` class, a pivotal part of the framework, encapsulates a wide array of functionalities ranging from basic operations like setting and getting pixel values to more advanced features like drawing geometric shapes (lines, rectangles, circles, Bezier curves), applying transformations (rotation, scaling, anti-aliasing), and performing image processing techniques (grayscale conversion, Gaussian blur, bloom effect). These capabilities make `ppmpp.hpp` a versatile tool for developers and artists, allowing for precise pixel-level manipulation and high-level graphic transformations.

* * *

## What?

Let’s delve deeper into the extensive features and capabilities of the `Modern C++20` framework.

### Exploring the Fundamental Types in ppmpp.hpp

The `ppmpp.hpp` framework introduces several fundamental types that form the backbone of its image processing capabilities. These types are carefully designed to represent key elements in graphics manipulation, ensuring both precision and ease of use.

#### Pixel: The Color Representation

The `Pixel` type is a cornerstone of the framework, defined as `std::tuple<double, double, double>.` Each `Pixel` instance represents a color, with the tuple holding three `double` values corresponding to the color’s red, green, and blue (RGB) components. This high-precision representation allows for a vast spectrum of colors, facilitating accurate color manipulation and rendering. The use of `double` for color values provides greater control over color gradients and transitions, essential for detailed image processing tasks.

#### Coord: Specifying Geometric Coordinates

The `Coord` type is `std::tuple<int, int, int, int>,` representing a set of coordinates within the image. Typically, this type defines the start and end points of lines or the boundaries of shapes. For example, in a line-drawing function, the first two integers might represent the starting point (x1, y1), and the latter two represent the line’s ending point (x2, y2). This type is integral for geometric manipulations, allowing for precise placement and transformation of shapes and lines within the image canvas.

#### Point: A Simple Coordinate Pair

The `Point type,` defined as `std::tuple<int, int>,` is a simplified version of `Coord,` representing a single point in 2D space with an x and y coordinate. It is particularly useful in scenarios where only a reference point is needed, such as marking a specific location on an image or defining a center point for circular shapes. The Point type is a fundamental building block in image processing, providing a straightforward way to handle individual points in various graphic operations.

These types, `Pixel,` `Coord,` and `Point,` are not just data structures but are central to the framework’s design philosophy, ensuring that complex image processing operations can be conducted with clarity and efficiency. Their implementation facilitates various applications, from basic pixel manipulation to advanced graphic transformations.

### Understanding the Helper Functions in ppmpp.hpp

The `ppmpp.hpp` framework is equipped with a suite of helper functions designed to simplify and streamline various tasks in image manipulation. These functions are grouped into different categories based on their functionalities:

#### Color Manipulation Functions

These functions are crucial for handling the color properties of pixels: `getFloatColorElement,` `getfRedColorElement,` `getfGreenColorElement,` `getfBlueColorElement:` These functions convert color elements from their integral representation to a floating-point format, facilitating precise color manipulation. They are essential for operations that require a higher degree of color accuracy, such as color blending or gradient creation.

`getRedColorElement,` `getGreenColorElement,` `getBlueColorElement:` In contrast, these functions convert color elements from a floating-point format back to their integral representation, useful for final rendering or when working with color formats that require integer values.

`createfPixelWithColor,` `createPixelWithColor:` These functions allow the creation of Pixel instances from individual color values, either in floating-point or integral formats. This is particularly useful for defining custom colors for drawing and image processing.

`createfGrayPixel` and `createGrayPixel:` These functions simplify the creation of grayscale pixels, which is useful in scenarios like generating grayscale images or applying grayscale filters.

#### Coordinate and Point Creation Functions

These functions are designed to create and manipulate geometric data: `createCoord` and `createCoordFromPoints:` These functions facilitate the creation of `Coord` objects, which are essential in defining geometric shapes and lines within the image.

`createPoint:` This function is used for creating `Point` objects, representing a single point in the image space, crucial for pinpointing locations or defining centers of shapes.

`getCoordX1,` `getCoordX2,` `getCoordY1,` `getCoordY2,` `getPointX1,` ```getPointY1``: These functions retrieve specific coordinates from Coord````` andPoint` `` objects, making it easier to access and manipulate individual coordinate values.

`getFirstPointFromCoord,` `getSecondPointFromCoord:` These functions extract `Point` objects from a `Coord` object, useful in scenarios where individual points must be isolated from a coordinate pair.

#### Direct Pixel Manipulation Functions

These functions allow direct modification of the color components of a pixel: `setRedColorElement,` `setGreenColorElement,` `setBlueColorElement:` These functions provide a way to directly set the red, green, or blue component of a pixel, either using floating-point or integral values. They are crucial for operations that require direct manipulation of pixel colors, such as image editing or filter applications.

### Exploring Color Helper Functions in ppmpp.hpp

The `ppmpp.hpp` framework offers a set of color helper functions extending its color manipulation capability, which is essential for advanced image processing and graphic design tasks. These functions focus on color blending and color space conversions, providing versatile tools for artists and developers.

#### Color Blending Function

`blendColors(Pixel &colorbackground, Pixel &colorforeground, float alpha):` This function is a cornerstone for creating composite images and effects. Based on an alpha value, it blends two colors – a background and a foreground color. The alpha parameter determines the opacity of the foreground color, allowing for seamless blending. This is particularly useful in creating translucent overlays, anti-aliasing, or mixing colors to achieve a desired visual effect.

#### Color Space Conversion Functions

`getHSV(double& h, double& s, double& v, const Pixel& px):` This function converts a color from its RGB representation to the HSV (Hue, Saturation, Value) color space. The HSV color model is often more intuitive for human perception, making adjusting brightness, saturation, or hue shifts easier. This function is vital for applications like color correction, artistic filters, or any scenario requiring more human-centric color manipulation.

`setHSV(double h, double s, double v, Pixel& px):` The counterpart to `getHSV,` this function takes hue, saturation, and value parameters and converts them back to an RGB representation in the `Pixel` format. This is particularly useful for applying changes made in the HSV space to an image or graphic that operates primarily in RGB, such as rendering the final output or interfacing with other graphic systems.

### Exploring Constructors and Operators of the Image Class in ppmpp.hpp

The `Image` class in the `ppmpp.hpp` framework is designed with a comprehensive set of constructors and operators, ensuring flexibility and ease of use in image manipulation and processing.

#### Constructors

Default Constructor (`Image()):` Initializes an empty image. This constructor is useful when an `Image` object must be declared without immediately assigning any specific data or dimensions.

Parameterized Constructor (`Image(int width, int height)):` Creates an image with specified dimensions. This constructor is essential for initializing an image with a predetermined size, providing a canvas for drawing or image processing.

Explicit Constructor (`explicit Image(std::string const& filename)):` Constructs an image by loading data from a specified file. This is particularly useful for working with existing images, allowing users to load and process images from the file system.

#### Copy Constructor and Assignment Operator

Copy Constructor (`Image(const Image& other)):` Creates a new `Image` instance as a copy of an existing one. This is vital for scenarios where an exact duplicate of an image is needed without affecting the original.

Copy Assignment Operator (`Image& operator=(const Image& other)):` Enables assigning one `Image` object to another, replacing its contents with those of the other object. This operator is crucial for straightforwardly copying image data.

#### Move Constructor and Assignment Operator

Move Constructor (`Image(Image&& other) noexcept):` Facilitates the transfer of an image from one object to another without copying the actual data, enhancing performance, especially for large images.

Move Assignment Operator (`Image& operator=(Image&& other) noexcept):` Similar to the move constructor, this operator transfers image data from one object to another, freeing up resources efficiently and ensuring optimal memory usage.

#### Comparison Operators

Equality (`friend bool operator==(const Image& lhs, const Image& rhs)):` Checks if two `Image` instances are equivalent, i.e., they have the exact dimensions and pixel data. This is useful for validating image processing results or checking if two images are identical.

Inequality (`friend bool operator!=(const Image& lhs, const Image& rhs)):` The opposite of the equality operator, it checks if two `Image` instances are different in terms of dimensions or pixel data. This can be useful in scenarios where image changes or differences need to be detected.

### Exploring the Public Methods of the Image Class in ppmpp.hpp

The `Image` class offers a comprehensive set of public methods, each tailored for specific image manipulation tasks:

#### Basic Image Manipulation Methods

`resize,` ``setWidth, ' and setHeight`:`` These methods provide fundamental control over the image’s dimensions, allowing users to resize images according to their needs.

`getWidth,` `getHeight:` Retrieve the current dimensions of the image, useful for calculations and conditional operations based on size.

#### Pixel Manipulation Methods

`setPixel,` `getPixel:` Directly manipulate individual pixels, setting or retrieving their color. It is essential for drawing, editing, or analyzing images at the pixel level.

`setAllPixels:` Uniformly sets the color of all pixels in the image, useful for initializing backgrounds or applying color filters.

`setImage,` `getImage:` Assign a new image data or retrieve the current data, enabling more complex image processing and transformations.

#### Drawing and Shape Methods

`drawLine,` `getAngledLine:` Draw straight or angled lines, fundamental for creating basic graphics or annotations.

`drawBezierQuadratic,` `drawBezierCubic:` Render Bezier curves, crucial for creating smooth curves and complex shapes.

`drawRectangle,` `drawFilledRectangle:` Create rectangles and filled rectangles, a basic yet versatile tool for graphical layouts and designs.

`drawCircle,` `drawFilledCircle,` `drawWedge,` `drawFilledWedge:` Draw circular shapes and segments important for pie charts, graphs, or decorative elements.

`drawTriangle` and `drawFilledTriangle:` Render triangles are fundamental geometric shapes with numerous applications in graphic design.

`drawRotatedRectangle,` `drawFilledRotatedRectangle,` `drawRotatedEllipse,` `drawFilledRotatedEllipse,` `drawRotatedPolygon,` `drawFilledRotatedPolygon:` These methods enable the creation of rotated geometric shapes, adding dynamism and variety to graphical compositions.

#### Advanced Image Processing Methods

`getAverageRgbOfImage:` Calculate the image’s average color, which is useful for color analysis or generating thumbnails.

`convertToGrayscale,` `applyGaussianBlur,` `applyAntiAliasing:` Apply essential image processing techniques like grayscale conversion, blurring, and anti-aliasing, which are crucial for creating artistic effects or enhancing image quality.

`downscale,` `upscale:` Resize the image with specific algorithms, which are vital for adapting images to different resolutions while maintaining quality.

`applyBloom,` `applyLens:` Implement advanced visual effects like bloom or lens effects, enhancing the visual appeal of images.

`drawGradients:` Create gradient effects, a key feature for backgrounds, buttons, or visual indicators.

#### File I/O Methods

`read,` `write:` Load and save images in PPM P6 format, ensuring compatibility and ease of data exchange with external sources and tools.

#### Private Member Variables

The `Image` class is defined with the following private member variables:

`std::vector<Pixel> m_img;:` This vector holds the image’s pixel data. Each `Pixel` in the vector represents an individual pixel’s color in the image, storing its red, green, and blue components.

`int m_width = 0;:` This integer stores the image’s width in pixels. It defines the horizontal dimension of the image, determining how many pixels are in each row of the `m_img` vector.

`int m_height = 0;:` Similar to `m_width,` this integer stores the height of the image, representing the vertical dimension. It determines the number of rows in the `m_img` vector.

* * *

## More Details

### Understanding the `blendColors` Function in ppmpp.hpp

The `blendColors` function is a sophisticated tool designed for blending two colors, a background and a foreground color, based on an alpha transparency value. This function is key to creating various visual effects and is pivotal in color-blending tasks.

#### Function Signature

`Pixel blendColors(Pixel &colorbackground, Pixel &colorforeground, float alpha):` The function takes two `Pixel` references – one for the background color and one for the foreground color – along with a floating-point `alpha` value representing the opacity of the foreground color.

#### Operational Logic

The function calculates the blended color by linearly interpolating between the foreground and background colors based on the `alpha` value. The alpha value ranges from 0.0 (fully transparent) to 1.0 (fully opaque).

For each color component (red, green, blue), the function applies the formula: Blended Component=(Foreground Component×alpha)+(Background Component×(1.0−alpha))Blended Component=(Foreground Component×alpha)+(Background Component×(1.0−alpha)) This ensures that each component of the resulting color is a weighted average of the corresponding components of the foreground and background colors.

The function then constructs a new `Pixel` object with the blended color components using `createfPixelWithColor.`

#### Practical Applications

Transparency and Overlays: Ideal for implementing transparency in images, allowing for the creation of overlay effects where the foreground image or color blends into the background.

Antialiasing and Smoothing: Useful in antialiasing where colors at edges are blended to create a smoother transition, reducing the jaggedness of lines and curves.

Artistic Effects: Enables the creation of various artistic effects, such as soft shadows, light glows, or color blending in digital painting applications.

#### Example Usage

Consider a scenario where you want to overlay a semi-transparent red color over a blue background. By calling `blendColors` with the blue color as `colorbackground,` the red color as `colorforeground,` and an alpha value of 0.5, the function will return a purple hue, effectively blending red and blue equally.

### Understanding `setHSV` and `getHSV` Functions in ppmpp.hpp

#### The `setHSV` Function

Purpose: Converts HSV color values to the RGB color model and sets these values to a given `Pixel.`

Implementation Details The function first checks if the saturation (s) is 0, implying a grayscale color, and sets the `Pixel` to the corresponding shade of gray based on the value (v).

The hue (h) is then adjusted to fit within the 0-360 degree range and converted to a 0-6 range to determine the RGB conversion segment.

The function calculates the RGB values using the HSV-to-RGB conversion formula based on the segment. This involves linear interpolation between two RGB components based on the hue’s position within its segment.

Usage Scenario: Use `setHSV` when you have color data in HSV format (often more intuitive for human perception) and need to convert it to RGB format for operations that require RGB values, like rendering on most displays.

#### The `getHSV` Function

#### Purpose

Extracts the HSV values from a given `Pixel’s` RGB color representation.

Implementation Details The function begins by extracting the RGB values from the `Pixel.`

It calculates the minimum and maximum values among the RGB components to determine the value (v) and the range (delta).

The saturation (s) is calculated from the delta and max values. If the max value is 0, indicating a black color, the saturation is set to 0.

The hue (h) is calculated based on which RGB component has the maximum value, adjusting the formula to find the correct hue angle.

Usage Scenario: `getHSV` is useful when you need to manipulate an image or color based on hue, saturation, or brightness levels – tasks that are often more straightforward in the HSV color space.

#### Practical Applications

Graphic Design and Image Processing: These functions are pivotal in applications that require color adjustments based on human color perception, like photo editing software or color pickers.

Data Visualization: They are also useful in scenarios where color gradients must be generated based on value or intensity (like heatmaps).

Art and Animation: Artists and animators can use these functions to create more natural and intuitive color transitions and effects.

* * *

## PPMPP: Image Processing Function Reference

### void setPixel(int xCoord, int yCoord, const Pixel& newPixel)

#### Purpose

The setPixel function is used to set the color of a specific pixel in the image to a new value.

#### Parameters

int xCoord: The x-coordinate of the pixel to be set.

int yCoord: The y-coordinate of the pixel to be set.

const Pixel& newPixel: The new color value for the pixel, represented as a `Pixel` object (which is a tuple of three doubles, each representing the red, green, and blue components of the color).

#### Functionality

Boundary Check: The function first checks if the specified coordinates (`xCoord` and `yCoord)` are within the boundaries of the image. This is determined by comparing `xCoord` with `0` and `m_width` and `yCoord` with `0` and `m_height.` Here, `m_width` and `m_height` are private member variables of the `Image` class that store the width and height of the image, respectively.

Pixel Update: If the coordinates are within the valid range, the function calculates the index corresponding to these coordinates in the `m_img` vector (which stores the image data) using the `getIndex` function. The `getIndex` function maps 2D coordinates to a 1D vector index. Once the index is determined, the function updates the pixel at this index with the new color value provided by `newPixel.`

#### Usage Example

```
1 Image myImage(100, 100); // Creating an image of 100x100 pixels
2 Pixel redColor = std::make_tuple(1.0, 0.0, 0.0); // Creating a red color
3 myImage.setPixel(50, 50, redColor); // Setting the pixel at (50, 50) to red
```

Figure 99

#### Remarks

The function ensures that the pixel coordinates are within the image bounds, preventing any out-of-range errors that could occur when accessing the `m_img` vector.

This method is fundamental for image drawing and editing operations, as it allows for manipulating individual pixels, the basic unit of a digital image.

* * *

### void getAngledLine(Coord& lineCoords, const Point& center, double degrees, int length)

#### Purpose

The `getAngledLine` function calculates the coordinates of a line segment based on a starting point, an angle, and a length. This function determines the end coordinates of a line that starts from a given point and extends at a specified angle for a certain length.

#### Parameters

`Coord& lineCoords:` A reference to a `Coord` tuple that will store the line’s calculated start and end coordinates.

`const Point& center:` The starting point of the line, given as a `Point` tuple containing the x and y coordinates.

`double degrees:` The angle at which the line extends from the starting point in degrees.

`int length:` The line length from the starting point.

#### Functionality

Angle Conversion: The function first converts the angle from degrees to radians, as the C++ trigonometric functions in ``` use radians. This conversion is done by multiplying the degree value by (pi/180).

Coordinate Calculation: Using trigonometry, the function calculates the end coordinates of the line. It adds the cosine of the angle (multiplied by the length) to the x-coordinate and the sine (also multiplied by the length) to the y-coordinate of the starting point.

Tuple Assignment: The start and end coordinates are then assigned to `lineCoords,` forming a `Coord` tuple, which typically consists of four integers representing a line segment’s starting and ending x and y coordinates.

#### Usage Example

```
1 Point center = std::make_tuple(50, 50); // Starting point at (50, 50)
2 double angle = 45; // Angle in degrees
3 int length = 100; // Length of the line
4 
5 Coord lineCoords;
6 getAngledLine(lineCoords, center, angle, length);
7 
8 // Now lineCoords contains the start and end coordinates of the line
```

Figure 100

#### Remarks

This function is particularly useful in graphics programming for drawing lines at specific angles, a common requirement in various applications like game development, simulations, or graphical representations.

The conversion to radians and trigonometric functions are essential to accurately determine the line’s direction and length based on the given angle.

* * *

### void drawBezierQuadratic(const Point& pt0, const Point& pt1, const Point& pt2, int split, const Pixel& bezierColor)

#### Purpose

The `drawBezierQuadratic` function draws a quadratic Bezier curve on an image. Bezier curves are widely used in computer graphics for modeling smooth curves and are fundamental in vector graphic designs.

#### Parameters

`const Point& pt0:` The first control point of the Bezier curve.

`const Point& pt1:` The second control point defines the curve’s tangent at the start and end points.

`const Point& pt2:` The third control point of the curve.

`int split:` The number of segments to divide the curve into. A higher value results in a more detailed curve.

`const Pixel& bezierColor:` The color of the Bezier curve, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

`Curve Calculation:` The function calculates the intermediate points of the quadratic Bezier curve based on the control points `pt0,` `pt1,` and `pt2.` It does this by linearly interpolating between these points for each fraction of the curve, determined by the `split` parameter.

`Coordinate Generation:` It generates a series of `(x, y)` coordinates representing the curve’s path and stores them in `xyCoordinates.`

`Drawing the Curve:` Once the coordinates are calculated, `drawXyLineImpl` is called to draw straight line segments between these coordinates using the specified `bezierColor.` This approximates the smooth Bezier curve.

#### Usage Example

```
1 Point pt0 = std::make_tuple(10, 10); // First control point
2 Point pt1 = std::make_tuple(50, 100); // Second control point
3 Point pt2 = std::make_tuple(100, 10); // Third control point
4 int split = 20; // Number of segments
5 Pixel bezierColor = std::make_tuple(1.0, 0.0, 0.0); // Red color
6 
7 drawBezierQuadratic(pt0, pt1, pt2, split, bezierColor);
8 // This will draw a quadratic Bezier curve on the image
```

Figure 101

#### Remarks

Quadratic Bezier curves are characterized by their simplicity and elegance, making them suitable for various graphic applications, from font rendering to animation paths.

The smoothness and accuracy of the curve are directly influenced by the `split` parameter, which determines how many line segments are used to approximate the curve.

This method efficiently adds complex shapes and paths to an image with minimal computational overhead.

* * *

### void drawBezierCubic(const Point& pt0, const Point& pt1, const Point& pt2, const Point& pt3, int split, const Pixel& bezierColor)

#### Purpose

The `drawBezierCubic` function is designed to draw a cubic Bezier curve on an image. For smooth and scalable curves, cubic Bezier curves are essential in computer graphics and digital animation.

#### Parameters

`const Point& pt0:` The first control point of the Bezier curve.

`const Point& pt1:` The second control point influences the tangent direction at the start point.

`const Point& pt2:` The third control point affects the tangent direction at the endpoint.

`const Point& pt3:` The fourth control point of the curve.

`int split:` Defines the number of line segments that approximate the curve, affecting its smoothness.

`const Pixel& bezierColor:` Specifies the color for the Bezier curve, represented as a Pixel object.

#### Functionality

Curve Calculation: The function employs `cubicBezierCurvesImpl` to compute intermediate points of the cubic Bezier curve using the control points ```pt0``, pt1````, pt2``, and pt3``` . The split` `` parameter determines the number of points calculated along the curve, impacting its resolution.

Coordinate Generation: A vector of ```(x, y)`` coordinates (xyCoordinates`)``` is generated, outlining the curve’s path.

Drawing the Curve: The `drawXyLineImpl` method draws line segments between the calculated coordinates, approximating the Bezier curve with the specified `bezierColor.`

#### Usage Example

```
1 Point pt0 = std::make_tuple(10, 10); // First control point
2 Point pt1 = std::make_tuple(30, 150); // Second control point
3 Point pt2 = std::make_tuple(150, 150); // Third control point
4 Point pt3 = std::make_tuple(170, 10); // Fourth control point
5 int split = 30; // Number of segments for curve approximation
6 Pixel bezierColor = std::make_tuple(0.0, 0.0, 1.0); // Blue color
7 
8 drawBezierCubic(pt0, pt1, pt2, pt3, split, bezierColor);
9 // Draws a cubic Bezier curve in blue
```

Figure 102

#### Remarks

Due to the additional control point, the cubic Bezier curve offers greater control over the curve shape than quadratic Bezier curves.

The function’s effectiveness in drawing complex shapes makes it particularly useful in graphic design, font rendering, and user interface development.

The precision and visual quality of the curve are contingent upon the `split` parameter, which should be chosen based on the desired level of detail and computational efficiency.

* * *

### void drawRectangle(const Point& xy, const Point& wh, const Pixel& rectangleColor)

#### Purpose

The `drawRectangle` function is designed to draw a rectangle on an image. This function is fundamental in computer graphics for creating basic shapes and forms, useful in a wide range of applications, from user interface design to complex image processing.

#### Parameters

`const Point& xy:` Represents the top-left corner of the rectangle, with

`xy` being a tuple indicating the `(x, y)` coordinates.

`const Point& wh:` Specifies the rectangle’s width (`w)` and height (`h).`

`const Pixel& rectangleColor:` Defines the rectangle’s color, represented as a Pixel object. The Pixel is a tuple of three doubles for the color’s red, green, and blue components.

#### Functionality

Drawing the Rectangle: The function internally calls `drawRectImpl,` passing the top-left corner coordinates, dimensions, and color of the rectangle.

Edge Calculation: `drawRectImpl` calculates the coordinates for the remaining corners of the rectangle based on the provided width and height.

Outline Rendering: The function then draws lines connecting these corners to form the outline in the specified `rectangleColor.`

#### Usage Example

```
1 Point topLeftCorner = std::make_tuple(50, 50); // Top-left corner of the rectangle
2 Point dimensions = std::make_tuple(100, 150); // Width and height of the rectangle
3 Pixel color = std::make_tuple(1.0, 0.0, 0.0); // Red color
4 
5 drawRectangle(topLeftCorner, dimensions, color);
6 // Draws a red rectangle with the top-left corner at (50, 50) and dimensions 100x150
```

Figure 103

#### Remarks

The function provides a simple yet effective way to draw rectangles, an essential element in many graphic and interface design tasks.

Ensuring that the rectangle’s dimensions and position are within the image’s bounds is essential to avoid errors.

The ability to define the rectangle’s color allows for versatility in design and visualization applications.

* * *

### void drawFilledRectangle(const Point& xy, const Point& wh, const Pixel& rectangleColor)

#### Purpose

The `drawFilledRectangle` function is designed to draw a filled rectangle on an image. This function is particularly useful in graphics programming for rendering solid shapes, creating backgrounds, or blocking out areas in an image.

#### Parameters

`const Point& xy:` Specifies the rectangle’s top-left corner.

`xy` is a tuple representing the `(x, y)` coordinates.

`const Point& wh:` Determines the rectangle’s width (`w)` and height (`h).`

`const Pixel& rectangleColor:` Sets the color of the rectangle. The Pixel is a tuple containing three double values, representing the color’s red, green, and blue components.

#### Functionality

Filling the Rectangle: The function invokes `drawFilledRectImpl,` passing the coordinates of the top-left corner, the dimensions, and the rectangle’s color.

Calculating Area: `drawFilledRectImpl` computes the entire area to be filled based on the width and height parameters.

Color Application: The function iteratively sets the pixel color for each point within the rectangle’s area to `rectangleColor,` effectively filling it.

#### Usage Example

```
1 Point topLeftCorner = std::make_tuple(30, 40); // Top-left corner of the rectangle
2 Point dimensions = std::make_tuple(200, 100); // Width and height of the rectangle
3 Pixel color = std::make_tuple(0.0, 0.0, 1.0); // Blue color
4 
5 drawFilledRectangle(topLeftCorner, dimensions, color);
6 // Draws a filled blue rectangle with its top-left corner at (30, 40) and dimensions\
7  200x100
```

Figure 104

#### Remarks

This method is essential for creating solid geometric shapes and can be used in various applications such as UI design, image processing, and graphic rendering.

Ensuring the rectangle’s position and dimensions fit within the image bounds is crucial to avoid potential out-of-bound errors.

Filling a rectangle with a specific color offers flexibility and creativity in graphic design and visualization tasks.

* * *

### void drawCircle(const Point& xy, int radius, const Pixel& circleColor)

#### Purpose

The `drawCircle` function draws a circle on the image. It defines the circle’s center, radius, and color.

#### Parameters

`const Point& xy:` A tuple representing the coordinates (x, y) of the circle’s center.

`int radius:` The radius of the circle.

`const Pixel& circleColor:` The color of the circle, represented as a Pixel object (which is a tuple of three doubles, each for red, green, and blue components).

#### Functionality

`Center and Radius Calculation:` The function identifies the circle’s center using the `xy` parameter and its radius through the `radius` parameter.

Drawing Algorithm: It is internally called `drawCircleImpl,` which likely uses a circle drawing algorithm (like Bresenham’s circle algorithm) to determine the pixels that form the circle’s outline.

Color Application: For each calculated pixel that forms the circle, the function sets its color to `circleColor.`

#### Usage Example

```
1 // Example to draw a circle
2 Point center = std::make_tuple(50, 50); // Center of the circle at (50, 50)
3 int radius = 10; // Radius of 10 units
4 Pixel color = std::make_tuple(1.0, 0.0, 0.0); // Red color
5 drawCircle(center, radius, color); // Drawing a red circle
```

Figure 105

#### Remarks

The function provides a simple and efficient way to add circular shapes to an image, which can be used in various graphical applications.

It’s important to ensure the circle’s parameters (center and radius) are within the image’s bounds to prevent out-of-range errors.

This method is essential for creating complex images and graphics where circular elements are needed.

* * *

### void drawFilledCircle(const Point& xy, int radius, const Pixel& circleColor)

#### Purpose

The `drawFilledCircle` function is designed to draw a filled circle on the image. This function specifies the circle’s center, radius, and fill color.

#### Parameters

`const Point& xy:` A tuple representing the coordinates (x, y) of the circle’s center.

`int radius:` The radius of the circle.

`const Pixel& circleColor:` The fill color for the circle, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Center and Radius Identification: The function uses the `xy` parameter to determine the center and the `radius` parameter to define the size of the circle.

Filling Algorithm: Internally, it is called `drawFilledCircleImpl, ’ which employs a circle drawing algorithm modified to fill the circle rather than outline it. This includes determining all the pixels within the radius from the center and setting their color.

Color Application: Each pixel within the specified radius is set to the `circleColor,` effectively filling the entire circle.

#### Usage Example

// Example of drawing a filled circle Point center = std::make_tuple(100, 100); // Center at (100, 100) int radius = 30; // Radius of 30 units Pixel fillColor = std::make_tuple(0.0, 0.0, 1.0); // Blue color drawFilledCircle(center, radius, fillColor); // Drawing a filled blue circle

#### Remarks

This function is essential for creating filled circular shapes, common in graphic design and image processing applications.

It’s crucial to ensure that the circle’s center and radius are within the image boundaries to prevent any out-of-bounds errors.

The method provides a fundamental capability for creating complex images, patterns, and designs that require filled circles.

* * *

### void drawWedge(const Point& center, int radius, int startAngle, int endAngle, const Pixel& wedgeColor)

#### Purpose

The `drawWedge` function is designed to draw a wedge (a sector of a circle) on the image. This function specifies the center of the circle from which the wedge is derived, the radius of the circle, the wedge’s starting and ending angles, and the wedge’s color.

#### Parameters

`const Point& center:` A tuple representing the coordinates (x, y) of the circle’s center from which the wedge is derived.

`int radius:` The radius of the circle.

`int startAngle,` `int endAngle:` The starting and ending angles for the wedge, in degrees. These angles define the sector of the circle that forms the wedge.

`const Pixel& wedgeColor:` The color of the wedge, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Center, Radius, and Angles: The function uses the `center` and `radius` parameters to determine the circle’s base and the `startAngle` and `endAngle` to specify the sector of the circle.

Wedge Drawing Algorithm: It is called `drawWedgeImpl, ’ which implements the logic to draw the specified sector of the circle. This involves calculating the points along the circumference between the start and end angles and then connecting these points to the center.

Color Application: The area defined by the sector is filled with the `wedgeColor,` effectively creating a colored wedge.

#### Usage Example

```
1 // Example of drawing a wedge
2 Point center = std::make_tuple(150, 150); // Center at (150, 150)
3 int radius = 50; // Radius of 50 units
4 int startAngle = 0; // Starting angle at 0 degrees
5 int endAngle = 90; // Ending angle at 90 degrees
6 Pixel wedgeColor = std::make_tuple(1.0, 0.0, 0.0); // Red color
7 drawWedge(center, radius, startAngle, endAngle, wedgeColor); // Drawing a red wedge
```

Figure 106

#### Remarks

This function is crucial for creating pie charts, circular gauges, and other graphics that require drawing the sectors of a circle.

The method provides flexibility in creating circular designs and patterns, offering a vital tool in graphic design and image processing applications.

* * *

### void drawFilledWedge(const Point& center, int radius, int startAngle, int endAngle, const Pixel& wedgeColor)

#### Purpose

The `drawFilledWedge` function is designed to draw a filled wedge (a sector of a circle) on the image. It specifies the center of the circle from which the wedge is derived, the radius, the wedge’s starting and ending angles, and the wedge’s color.

#### Parameters

`const Point& center:` A tuple representing the coordinates (x, y) of the circle’s center from which the wedge is derived.

`int radius:` The radius of the circle.

`int startAngle,` `int endAngle:` The starting and ending angles for the wedge, measured in degrees. These define the sector of the circle that will be filled to create the wedge.

`const Pixel& wedgeColor:` The color for filling the wedge, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Sector Identification: The function identifies the circle sector to be filled using the `center,` `radius,` `startAngle,` and `endAngle` parameters.

Filling Algorithm: It is internally called `drawFilledWedgeImpl,` which employs an algorithm to fill the circle sector defined by the specified angles. This involves calculating the set of pixels within the industry defined and setting their color to `wedgeColor.`

Color Application: Every pixel within the specified sector is colored with `wedgeColor,` resulting in a filled wedge.

#### Usage Example

```
1 // Example of drawing a filled wedge
2 Point center = std::make_tuple(200, 200); // Center at (200, 200)
3 int radius = 40; // Radius of 40 units
4 int startAngle = 45; // Starting angle at 45 degrees
5 int endAngle = 135; // Ending angle at 135 degrees
6 Pixel wedgeColor = std::make_tuple(0.0, 1.0, 0.0); // Green color
7 drawFilledWedge(center, radius, startAngle, endAngle, wedgeColor); // Drawing a fill\
8 ed green wedge
```

Figure 107

#### Remarks

This function is particularly useful for creating pie chart segments, fan shapes, and other circular designs that require filled sectors.

This method extends the graphical capabilities of the library, allowing for more complex and visually appealing designs and patterns.

* * *

### void drawTriangle(const Point& pt1, const Point& pt2, const Point& pt3, const Pixel& triangleColor)

#### Purpose

The `drawTriangle` function is tailored to render a triangle on the image. It specifies the vertices of the triangle and its outline color.

#### Parameters

`const Point& pt1,` `const Point& pt2,` `const Point& pt3:` Tuples representing the coordinates of the triangle’s three vertices. Each point is a tuple (x, y) indicating the position of each vertex.

`const Pixel& triangleColor:` The color for the triangle’s outline, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Vertex Identification: To define the triangle’s vertices, the function utilizes the `pt1,` `pt2,` and `pt3` parameters.

Outline Drawing Algorithm: It internally invokes `drawTriangleImpl,` which implements the logic for outlining the triangle. This includes calculating the lines connecting each pair of vertices and setting their color to `triangleColor.`

Color Application: The triangle outline is drawn using `triangleColor,` creating a visually distinct triangular shape.

#### Usage Example

```
1 // Example of drawing a triangle
2 Point vertex1 = std::make_tuple(50, 50);  // Vertex 1 at (50, 50)
3 Point vertex2 = std::make_tuple(100, 100); // Vertex 2 at (100, 100)
4 Point vertex3 = std::make_tuple(50, 150); // Vertex 3 at (50, 150)
5 Pixel outlineColor = std::make_tuple(1.0, 0.5, 0.0); // Orange color
6 drawTriangle(vertex1, vertex2, vertex3, outlineColor); // Drawing an orange triangle
```

Figure 108

#### Remarks

This function is vital for creating triangular shapes, which are fundamental in various graphic designs and image-processing tasks.

The `drawTriangle` method is essential for constructing geometric patterns and complex images that involve triangular elements.

* * *

### void drawFilledTriangle(const Point& pt1, const Point& pt2, const Point& pt3, the Pixel& fillColor)

#### Purpose

The `drawFilledTriangle` function is specifically crafted to render a filled triangle on the image. It specifies the triangle’s vertices and the color used to fill it.

#### Parameters

`const Point& pt1,` `const Point& pt2,` `const Point& pt3:` These parameters represent the coordinates of the triangle’s three vertices. Each point is a tuple (x, y), indicating the position of each vertex.

`const Pixel& fillColor:` The color used to fill the triangle, expressed as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Vertex Identification: The function utilizes `pt1,` `pt2,` and `pt3` to define the triangle’s vertices.

Filling Algorithm: It internally calls `drawFilledTriangleImpl,` which implements an algorithm to fill the triangle area defined by the specified vertices. This includes determining all the pixels within the triangle’s boundaries and setting their color to `fillColor.`

Color Application: The triangle’s interior is filled with `fillColor,` effectively creating a solid-colored triangular shape.

#### Usage Example

```
1 // Example of drawing a filled triangle
2 Point vertex1 = std::make_tuple(120, 120); // Vertex 1 at (120, 120)
3 Point vertex2 = std::make_tuple(200, 200); // Vertex 2 at (200, 200)
4 Point vertex3 = std::make_tuple(120, 280); // Vertex 3 at (120, 280)
5 Pixel fillColor = std::make_tuple(0.5, 0.0, 0.5); // Purple color
6 drawFilledTriangle(vertex1, vertex2, vertex3, fillColor); // Drawing a filled purple\
7  triangle
```

Figure 109

#### Remarks

This function is crucial for creating filled triangular shapes, a basic yet versatile element in various graphic design and image processing applications.

The `drawFilledTriangle` method is fundamental for constructing geometric patterns, complex graphics, and designs that incorporate filled triangular elements.

* * *

### void drawRotatedRectangle(int x, int y, int w, int h, double angle, const Pixel& px)

#### Purpose

The `drawRotatedRectangle` function is crafted to render a rotated rectangle on the image. It specifies the rectangle’s position, dimensions, rotation angle, and fill color.

#### Parameters

`int x,` `int y:` The coordinates (x, y) representing the center of the rectangle.

`int w,` `int h:` The rectangle’s width (w) and height (h).

`double angle:` The rotation angle of the rectangle, in degrees, measured from the horizontal axis.

`const Pixel& px:` The color of the rectangle, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Position and Dimension Identification: The function uses the `x,` `y,` `w,` and `h` parameters to determine the position and size of the rectangle.

Rotation and Drawing Algorithm: Internally, it invokes `drawRotatedRectangleImpl,` which implements the logic to draw a rectangle rotated by the specified angle. This involves calculating the rotated positions of the rectangle’s corners and drawing the sides accordingly.

Color Application: The rectangle is filled with the color specified by `px,` resulting in a rotated, colored rectangle.

#### Usage Example

```
1 // Example of drawing a rotated rectangle
2 int centerX = 150; // Center X coordinate
3 int centerY = 150; // Center Y coordinate
4 int width = 100;   // Width of 100 units
5 int height = 50;   // Height of 50 units
6 double rotationAngle = 45.0; // Rotate by 45 degrees
7 Pixel rectangleColor = std::make_tuple(0.0, 0.5, 0.5); // Teal color
8 drawRotatedRectangle(centerX, centerY, width, height, rotationAngle, rectangleColor)\
9 ; // Drawing a rotated teal rectangle
```

Figure 110

#### Remarks

This function is vital for creating rectangles with a specified orientation, an essential feature in graphic designs, geometric patterns, and various image processing tasks.

Correctly calculating the rotated positions of the rectangle’s corners is critical to ensure the accuracy of the rotation effect.

The `drawRotatedRectangle` method extends the graphical capabilities of the library, allowing for more dynamic and visually exciting designs and patterns that incorporate rotated rectangular elements.

* * *

### void drawFilledRotatedRectangle(int x, int y, int w, int h, double angle, const Pixel& px)

#### Purpose

The `drawFilledRotatedRectangle` function aims to render a filled, rotated rectangle on the image. This function specifies the rectangle’s center coordinates, dimensions, rotation angle, and fill color.

#### Parameters

`int x,` `int y:` Coordinates (x, y) representing the center of the rectangle.

`int w,` `int h:` The rectangle’s width (w) and height (h), indicating its size.

`double angle:` The rotation angle of the rectangle in degrees, determining its orientation.

`const Pixel& px:` The fill color for the rectangle, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Center, Size, and Rotation Specification: The function uses `x,` `y,` `w,` `h,` and `angle` parameters to define the rectangle’s center position, size, and orientation.

Filling and Rotation Algorithm: It internally calls `drawFilledRotatedRectangleImpl,` which employs an algorithm to draw and fill a rectangle rotated by the specified angle. This includes calculating the transformed coordinates of the rectangle’s corners due to rotation and filling the resulting shape.

Color Application: The entire area of the rotated rectangle is set to the color specified by `px,` creating a solid-colored, rotated rectangular shape.

#### Usage Example

```
1 // Example of drawing a filled rotated rectangle
2 int centerX = 200; // Center X coordinate
3 int centerY = 100; // Center Y coordinate
4 int width = 120;   // Width of 120 units
5 int height = 60;   // Height of 60 units
6 double rotationAngle = 30.0; // Rotate by 30 degrees
7 Pixel rectangleColor = std::make_tuple(0.7, 0.3, 0.5); // A shade of purple
8 drawFilledRotatedRectangle(centerX, centerY, width, height, rotationAngle, rectangle\
9 Color); // Drawing a filled, rotated purple rectangle
```

Figure 111

#### Remarks

This function is crucial for creating dynamic and visually engaging designs that require rotated rectangles with filled colors, commonly used in various graphic designs and image processing tasks.

The accurate computation of the rotated positions of the rectangle’s corners is essential for ensuring the correct orientation and shape of the rectangle after rotation.

The `drawFilledRotatedRectangle` method enhances the creative possibilities within the library, allowing for more complex and aesthetically pleasing designs that include filled, rotated rectangular elements.

* * *

### void drawRotatedEllipse(int x, int y, int w, int h, double angle, const Pixel& px)

#### Purpose

The `drawRotatedEllipse` function is intended to render a rotated ellipse on the image. It specifies the ellipse’s center coordinates, dimensions, rotation angle, and fill color.

#### Parameters

`int x,` `int y:` Coordinates (x, y) representing the center of the ellipse.

`int w,` `int h:` The ellipse’s width (w) and height (h), defining its shape.

`double angle:` The rotation angle of the ellipse in degrees, determining its orientation.

`const Pixel& px:` The fill color for the ellipse, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Center, Shape, and Rotation Definition: The function uses `x,` `y,` `w,` `h,` and `angle` parameters to establish the ellipse’s central position, size, and rotation angle.

Drawing and Rotation Algorithm: It is internally called `drawRotatedEllipseImpl,` which implements an algorithm for drawing and filling an ellipse that the specified angle has rotated. This includes calculating the transformed coordinates of the ellipse’s boundary due to rotation and filling in the shape.

Color Application: The entire area of the rotated ellipse is colored with `px,` resulting in a solid-colored, rotated elliptical shape.

#### Usage Example

```
1 // Example of drawing a rotated ellipse
2 int centerX = 250; // Center X coordinate
3 int centerY = 150; // Center Y coordinate
4 int width = 100;   // Width of 100 units
5 int height = 60;   // Height of 60 units
6 double rotationAngle = 45.0; // Rotate by 45 degrees
7 Pixel ellipseColor = std::make_tuple(1.0, 0.0, 0.0); // Red color
8 drawRotatedEllipse(centerX, centerY, width, height, rotationAngle, ellipseColor); //\
9  Drawing a rotated red ellipse
```

Figure 112

#### Remarks

This function is precious for creating varied geometric shapes and designs, as rotated ellipses are commonly used in graphic design and image processing tasks.

Correctly determining the rotated positions of the ellipse’s boundary is crucial to ensure the accuracy of the rotation effect.

The `drawRotatedEllipse` method broadens the library’s creative design scope, creating more dynamic and visually appealing patterns and designs that incorporate rotated elliptical elements.

* * *

### void drawFilledRotatedEllipse(int x, int y, int w, int h, double angle, const Pixel& px)

#### Purpose

The `drawFilledRotatedEllipse` function is crafted to draw a filled and rotated ellipse on the image. This function specifies the ellipse’s center coordinates, dimensions, rotation angle, and fill color.

#### Parameters

`int x,` `int y:` Coordinates (x, y) representing the center of the ellipse.

`int w,` `int h:` The width (w) and height (h) of the ellipse, defining its overall shape.

`double angle:` The rotation angle of the ellipse in degrees determines its orientation.

`const Pixel& px:` The color used to fill the ellipse, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Center and Dimension Determination: The function uses `x,` `y,` `w,` and `h` parameters to establish the ellipse’s central position and size.

Filling and Rotation Process: Internally, it is called `drawFilledRotatedEllipseImpl,` which implements an algorithm for drawing and filling a rotated ellipse. This involves calculating the transformed coordinates of the ellipse’s boundary due to the rotation and filling in the resulting shape.

Color Application: The entire area within the boundary of the rotated ellipse is colored with `px,` resulting in a filled, colored, and rotated elliptical shape.

#### Usage Example

```
1 // Example of drawing a filled, rotated ellipse
2 int centerX = 200; // Center X coordinate
3 int centerY = 100; // Center Y coordinate
4 int width = 140;   // Width of 140 units
5 int height = 80;   // Height of 80 units
6 double rotationAngle = 30.0; // Rotate by 30 degrees
7 Pixel ellipseColor = std::make_tuple(0.0, 1.0, 0.0); // Green color
8 drawFilledRotatedEllipse(centerX, centerY, width, height, rotationAngle, ellipseColo\
9 r); // Drawing a filled, rotated green ellipse
```

Figure 113

#### Remarks

This function is essential for generating diverse and aesthetically appealing shapes, as filled, rotated ellipses are frequently utilized in various graphic designs and image processing projects.

Accurate calculation of the rotated positions of the ellipse’s boundary ensures the correct orientation and appearance of the ellipse after rotation.

The `drawFilledRotatedEllipse` method expands the library’s capabilities, allowing for more intricate and visually striking designs that include filled, rotated elliptical elements.

* * *

### void drawRotatedPolygon(const std::vector& vertices, double angle, const Pixel& px)

#### Purpose

The `drawRotatedPolygon` function is designed to draw a rotated polygon on the image. This function specifies the polygon’s vertices, the rotation angle, and the outline color.

#### Parameters

`const std::vector<Point>& vertices:` A vector of tuples, each representing the coordinates (x, y) of a vertex of the polygon.

`double angle:` The rotation angle of the polygon in degrees, determining its orientation.

`const Pixel& px:` The color of the polygon’s outline, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Vertex Identification: The function uses the `vertices` parameter to define the shape of the polygon.

Rotation Algorithm: Internally, it is called `drawRotatedPolygonImpl, ‘ which implements the logic for rotating the polygon by the specified angle. This involves calculating the new positions of the vertices after rotation and connecting these vertices to form the polygon.

Outline Color Application: The polygon’s outline is drawn using the color specified by `px,` creating a visually distinct polygonal shape.

#### Usage Example

```
 1 // Example of drawing a rotated polygon
 2 std::vector<Point> vertices = {
 3     std::make_tuple(100, 100),
 4     std::make_tuple(150, 130),
 5     std::make_tuple(120, 180),
 6     std::make_tuple(80, 180),
 7     std::make_tuple(50, 130)
 8 }; // Coordinates for a pentagon
 9 double rotationAngle = 45.0; // Rotate by 45 degrees
10 Pixel outlineColor = std::make_tuple(0.5, 0.5, 0.5); // Grey color
11 drawRotatedPolygon(vertices, rotationAngle, outlineColor); // Drawing a rotated grey\
12  pentagon
```

Figure 114

#### Remarks

This function is crucial for creating rotated polygonal shapes, a fundamental component in various graphic designs and image processing applications.

Accurate calculation of the new vertex positions post-rotation is essential to maintain the correct shape and orientation of the polygon.

The `drawRotatedPolygon` method provides a versatile tool for creating complex geometric patterns and designs involving rotated polygonal elements.

* * *

### void drawFilledRotatedPolygon(const std::vector& vertices, double angle, const Pixel& px)

#### Purpose

The `drawFilledRotatedPolygon` function is designed to draw a filled and rotated polygon on the image. This function specifies the polygon’s vertices, the rotation angle, and the fill color.

#### Parameters

`const std::vector<Point>& vertices:` A vector of tuples, each representing the coordinates (x, y) of a vertex of the polygon.

`double angle:` The rotation angle of the polygon in degrees, determining its orientation.

`const Pixel& px:` The color used to fill the polygon, represented as a Pixel object (a tuple of three doubles for red, green, and blue components).

#### Functionality

Vertex Identification and Rotation: The function uses the `vertices` parameter to define the shape of the polygon and the `angle` parameter to determine its rotation.

Filling and Rotation Process: Internally, it is called `drawFilledRotatedPolygonImpl, ’ which implements an algorithm for drawing and filling a rotated polygon. This involves calculating the new positions of the vertices after rotation and then filling the resulting shape.

Color Application: The entire area within the boundary of the rotated polygon is colored with `px,` resulting in a filled, colored, and rotated polygonal shape.

#### Usage Example

```
 1 // Example of drawing a filled, rotated polygon
 2 std::vector<Point> vertices = {
 3     std::make_tuple(150, 150),
 4     std::make_tuple(200, 175),
 5     std::make_tuple(175, 225),
 6     std::make_tuple(125, 225),
 7     std::make_tuple(100, 175)
 8 }; // Coordinates for a pentagon
 9 double rotationAngle = 30.0; // Rotate by 30 degrees
10 Pixel fillColor = std::make_tuple(0.25, 0.5, 0.75); // A shade of blue
11 drawFilledRotatedPolygon(vertices, rotationAngle, fillColor); // Drawing a filled, r\
12 otated blue pentagon
```

Figure 115

#### Remarks

This function is vital for creating complex and visually appealing shapes, as filled, rotated polygons are frequently used in various graphic designs and image processing projects.

Accurate calculation of the new vertex positions post-rotation is essential to maintain the correct shape and orientation of the polygon.

The `drawFilledRotatedPolygon` method expands the library’s capabilities, allowing for more intricate and artistically interesting designs that include filled, rotated polygonal elements.

* * *

### Pixel getAverageRgbOfImage()

#### Purpose

The `getAverageRgbOfImage` function is designed to calculate the average RGB color of the entire image. This function aggregates the color values of all pixels in the image and computes their average.

#### Parameters

None.

#### Functionality

Color Summation: The function iterates through each pixel in the image, represented by the `m_img` data structure. It accumulates the red (r), green (g), and blue (b) components of each pixel separately.

Average Calculation: After summing the color components of all pixels, it calculates the average for each color component (red, green, and blue) by dividing the total sum by the number of pixels in the image.

Average Color Creation: The function returns a Pixel object representing the average color. This Pixel is created using the calculated average values for the red, green, and blue components.

#### Usage Example

```
1 // Example of getting the average color of an image
2 Pixel averageColor = getAverageRgbOfImage();
3 std::cout << "Average Color - Red: " << std::get<0>(averageColor) << ", Green: " << \
4 std::get<1>(averageColor) << ", Blue: " << std::get<2>(averageColor) << std::endl;
```

Figure 116

#### Remarks

This function is handy for image analysis and processing applications where understanding the overall color tone of an image is necessary.

It provides a simple yet effective way to summarize the color information of an entire image into a single representative color.

The `getAverageRgbOfImage` method is a fundamental tool for applications in color balancing, filtering, and thematic studies in digital image processing.

* * *

### void convertToGrayscale()

#### Purpose

The `convertToGrayscale` function is designed to convert the entire image to grayscale. This function modifies the color of each pixel in the image to its grayscale equivalent, resulting in an image composed entirely of shades of gray.

#### Parameters

None.

#### Functionality

Grayscale Conversion: The function internally calls `convertToGrayscaleImpl,` which implements the grayscale conversion algorithm. This algorithm typically involves calculating the luminance of each pixel by considering its red, green, and blue components and then setting all three components to this luminance value.

Pixel-by-Pixel Processing: It iterates over each pixel in the image, adjusting the color values so that the red, green, and blue components of each pixel are equal, resulting in a shade of gray that corresponds to the original pixel’s brightness.

#### Usage Example

```
1 // Example of converting an image to grayscale
2 convertToGrayscale(); // The entire image is now in grayscale
```

Figure 117

#### Remarks

This function is crucial in various image-processing tasks where color information is not essential, such as edge detection, texture analysis, and other forms of pattern recognition.

Converting to grayscale simplifies the image data, often making subsequent processing tasks more computationally efficient.

The `convertToGrayscale` method is a foundational tool in image processing, especially useful in scenarios where the focus is on intensity or brightness variation rather than color variation.

* * *

### void applyGaussianBlur()

#### Purpose

The `applyGaussianBlur` function is tailored to apply a Gaussian blur effect to the entire image. Gaussian blur is a widely used effect in image processing that smooths out images by averaging the pixels within a region, reducing noise and detail.

#### Parameters

None.

#### Functionality

Gaussian Blur Algorithm: The function internally invokes `applyGaussianBlurImpl,` which implements the Gaussian blur algorithm. This algorithm typically involves convolving the image with a Gaussian kernel, a mathematical function used to weight the average of the pixels based on their spatial distance from the center of the kernel.

Pixel-by-Pixel Processing: It processes each pixel in the image, considering the neighboring pixels to compute a blurred (smoothed) value. The extent of blurring depends on the size and standard deviation of the Gaussian kernel used in the algorithm.

#### Usage Example

```
1 // Example of applying Gaussian blur to an image
2 applyGaussianBlur(); // The entire image is now blurred
```

Figure 118

#### Remarks

This function is pivotal in various image processing tasks where reducing high-frequency noise or smoothing details is necessary, such as in pre-processing steps for edge detection or creating artistic effects.

Applying Gaussian blur can enhance the performance of algorithms sensitive to noise or fine details by providing a smoother version of the image.

The `applyGaussianBlur` method is a fundamental tool in digital image processing. It is widely used for its effectiveness in creating a visually pleasing blur effect mimicking how cameras capture out-of-focus points of light.

* * *

### void applyAntiAliasing()

#### Purpose

The `applyAntiAliasing` function is designed to smooth out the jagged edges in the image, often referred to as “aliasing.” This function applies an anti-aliasing technique to enhance the image’s visual quality by reducing the stair-step-like lines that can occur in digital images.

#### Parameters

None.

#### Functionality

Anti-Aliasing Algorithm: The function internally calls `applyAntiAliasingImpl,` which implements the anti-aliasing algorithm. This process typically involves averaging the pixel colors at the boundaries to create a smoother transition between edges.

Pixel Processing: It adjusts the color of the pixels along the edges of shapes within the image. By blending the colors of these edge pixels with their surrounding pixels, the function reduces the contrast that leads to the perception of jagged edges.

#### Usage Example

```
1 // Example of applying anti-aliasing to an image
2 applyAntiAliasing(); // The entire image now has smoother edges
```

Figure 119

#### Remarks

This function is essential in graphics rendering and digital image processing, where the presence of jagged edges can detract from the visual appeal and realism of images.

Anti-aliasing is crucial in preparing images for high-quality presentations, print media, or any other applications where image clarity and smoothness are desired.

The `applyAntiAliasing` method is a fundamental tool in image processing, improving the aesthetics of digital images by reducing the harshness of pixelated edges.

* * *

### void upscale(int scale)

#### Purpose

The `upscale` function is designed to increase the size of the image by a specified scale factor. This function enlarges the image, enhancing its dimensions while maintaining its aspect ratio.

#### Parameters

`int scale:` The factor by which the image’s dimensions will be multiplied. A scale factor greater than 1 enlarges the image, while a factor less than one would technically reduce its size.

#### Functionality

Scaling Process: The function internally calls `upscaleImpl,` which implements the scaling algorithm. This process involves resizing the image to a new set of dimensions, determined by multiplying the original dimensions by the scale factor.

Pixel Interpolation: During the scaling process, the algorithm interpolates new pixel values to maintain the image’s quality and details. This can involve techniques like bilinear or bicubic interpolation, which estimate new pixel values based on the surrounding pixels.

#### Usage Example

```
1 // Example of upscaling an image
2 int scaleFactor = 2; // Scaling the image to double its size
3 upscale(scaleFactor); // The image is now upscaled by a factor of 2
```

Figure 120

#### Remarks

This function is crucial for applications that require high-resolution images from lower-resolution sources. It is widely used in graphic design, media production, and other areas where image clarity at larger sizes is necessary.

While upscaling can increase the size of an image, it’s important to note that the quality of the upscaled image may sometimes match the clarity of a naturally high-resolution image due to the interpolation of new pixel values.

The `upscale` method provides a fundamental capability for resizing images, an essential process in various image manipulation and enhancement tasks.

* * *

### void applyBloom(double threshold, double sigma)

#### Purpose

The `applyBloom` function is designed to add a bloom effect to the image, a common technique in graphics processing that creates a soft glow around bright areas. This function uses a specified threshold to identify bright areas and applies a Gaussian blur characterized by the sigma value to create the bloom effect.

#### Parameters

`double threshold:` A value determining the brightness threshold for applying the bloom effect. Pixels brighter than this threshold will contribute to the bloom.

`double sigma:` The standard deviation of the Gaussian blur applied to create the bloom effect. A higher sigma value results in a softer, more spread-out glow.

#### Functionality

Brightness Identification: The function identifies pixels that exceed the specified brightness threshold in the image. These pixels are the source of the bloom effect.

Gaussian Blur Application: Internally, it is called `applyBloomImpl, ’ which applies a Gaussian blur to the bright areas. The extent of the blur is determined by the sigma value, affecting the softness and spread of the bloom effect.

Bloom Effect Creation: The blurred bright areas are combined with the original image, creating a glow effect around these areas.

#### Usage Example

```
1 // Example of applying a bloom effect to an image
2 double brightnessThreshold = 0.7; // Threshold for brightness
3 double blurSigma = 5.0; // Sigma for Gaussian blur
4 applyBloom(brightnessThreshold, blurSigma); // Applying the bloom effect
```

Figure 121

#### Remarks

The bloom effect is particularly popular in digital photography, video games, and film to simulate how bright light behaves on a real-world camera lens.

Applying bloom can enhance the visual appeal of an image by adding a dreamy, soft light quality to high-brightness areas.

The `applyBloom` method is a fundamental tool in advanced image processing, adding a layer of artistic depth and realism to digital images.

* * *

### void applyLens(int numb)

#### Purpose

The `applyLens` function is designed to simulate the effect of multiple lens distortions on the image. This function applies a specified number of lens effects, each creating a localized distortion that mimics the bending of light, akin to viewing through a convex or concave lens.

#### Parameters

`int numb:` The number of lens effects to be applied to the image. Each lens effect creates a localized distortion.

#### Functionality

Lens Effect Application: The function internally calls `applyLensImpl,` which implements the algorithm for applying lens distortions. This involves selecting random points in the image and distorting the surrounding pixels to create a lens-like effect.

Randomized Distortion: Each lens effect is applied at a random location on the image, and the extent of the distortion is based on predefined characteristics of the lens, such as its radius and refractive properties.

#### Usage Example

```
1 // Example of applying lens effects to an image
2 int numberOfLenses = 5; // Applying 5 lens effects
3 applyLens(numberOfLenses); // The image now has five localized lens distortions
```

Figure 122

#### Remarks

The lens effect is commonly used in graphical applications to create artistic and visually interesting distortions, simulating how light behaves when passing through curved glass.

This function adds a creative tool to the image processing library, allowing users to experiment with optical effects and enhance the visual appeal of their images.

The `applyLens` method is a versatile tool for adding a touch of realism or artistic flair to digital images, suitable for various applications in graphic design, digital art, and photo editing.

* * *

### void drawGradients(const std::vector& colors, double angle_degree)

#### Purpose

The `drawGradients` function is designed to draw a gradient on the image using a specified set of colors and an angle. This function creates a smooth transition between the provided colors across the image at a given angle.

#### Parameters

`const std::vector<Pixel>& colors:` A vector of Pixel objects, each representing a color. These colors are used to create the gradient.

`double angle_degree:` The angle in degrees at which the gradient is applied. This determines the direction of the color transition in the gradient.

#### Functionality

Color Transition: The function uses the `colors` parameter to define the sequence of colors that will be blended to form the gradient.

Angle-Based Rendering: It internally calls `drawGradientsImpl,` which employs an algorithm to apply the gradient at the specified `angle_degree.` This involves calculating the color values at each point in the image based on their position relative to the gradient direction.

Gradient Creation: The gradient is rendered across the image, smoothly transitioning between the specified colors in the direction set by the angle.

#### Usage Example

```
1 // Example of drawing a gradient
2 std::vector<Pixel> gradientColors = {
3     std::make_tuple(1.0, 0.0, 0.0), // Red
4     std::make_tuple(0.0, 1.0, 0.0), // Green
5     std::make_tuple(0.0, 0.0, 1.0)  // Blue
6 }; // Red to Green to Blue gradient
7 double angle = 45.0; // Gradient at a 45-degree angle
8 drawGradients(gradientColors, angle); // Drawing the gradient
```

Figure 123

#### Remarks

This function is invaluable for visually appealing backgrounds, design elements, graphics, and image processing effects.

Gradients are widely used for adding depth, dimension, and visual interest to images and graphical interfaces.

The `drawGradients` method provides a versatile tool for graphic designers and image processors to enhance their work with smooth, colorful transitions, adding a layer of sophistication to digital creations.

* * *

### void read(const std::string& filename)

#### Purpose

The `read` function is specifically designed to load an image from a file into the program, focusing on handling.PPM P6 file format. This function reads the image data from the specified.PPM file, allowing it to be processed and manipulated within the program.

#### Parameters

`const std::string& filename:` A string representing the path and name of the.PPM file to be read.

#### Functionality

File Format Specificity: The function is tailored to work with.PPM (Portable Pixmap) P6 files are a format known for its simplicity in storing pixel data.

Image Data Loading: Internally, it is called `readImpl, ‘ which implements the procedure for opening and decoding the.PPM P6 file. This process involves parsing the header for dimensions and color information and reading the binary pixel data into an appropriate image data structure in the program.

Error and Format Handling: The function includes mechanisms to handle common issues such as file not found, access permissions, and file format errors, ensuring robustness and reliability.

#### Usage Example

```
1 // Example of reading a .PPM P6 image file
2 std::string ppmFilePath = "path/to/image.ppm"; // Path to the .PPM file
3 image.read(ppmFilePath); // Loading the .PPM image into the program
```

Figure 124

#### Remarks

This function is an essential tool for applications that need to work with. PPM P6 format images are commonly used in various graphics and image processing tasks due to its straightforward binary format.

It is understanding the specifics of the.PPM format (such as its header structure and binary data layout) is crucial for correctly implementing and using this function.

The `read` method broadens the scope of the program’s image formats, making it versatile in dealing with different types of image data sources.

* * *

### void write(const std::string& filename)

#### Purpose

The `write` function saves the current image to a file.PPM (Portable Pixmap) P6 format. This function takes the current image data within the program and writes it to a specified file, allowing for external storage and further use.

#### Parameters

`const std::string& filename:` A string representing the path and name of the file where the image is to be saved.

#### Functionality

File Format Specification: The function is specifically tailored to handle the. PPM P6 file format is known for its straightforward binary format for storing pixel data.

Image Data Saving: Internally, it is called `writeImpl, ‘ which implements the process of converting the internal image data into the.PPM P6 format and writing it to a file. This includes creating the.PPM header and accurately writing the binary pixel data.

Error Handling and File Creation: The function includes error handling to manage scenarios such as inaccessible file paths or write permissions. It ensures that the file is created and saved correctly.

#### Usage Example

```
1 // Example of writing an image to a .PPM P6 file
2 std::string ppmFilePath = "path/to/output.ppm"; // Destination path for the .PPM file
3 image.write(ppmFilePath); // Saving the image as a .PPM P6 file
```

Figure 125

#### Remarks

This function is crucial for exporting images from the program, especially in scenarios where the.PPM format is required due to its simplicity and compatibility with various image processing tools.

Understanding the format specifications of. PPM P6, including header format and binary data encoding, is important for correctly implementing this function.

The `write` method adds essential functionality to the program, enabling users to easily save their processed images in a widely used and easy-to-handle format.

* * *

![](resources/nueende.jpg)

Figure 126

# Where To Go from Here

Having mastered the fundamentals of 2D computer graphics, you’re well-positioned to explore more advanced and diverse areas in this field. One logical progression is delving into 3D computer graphics. While 2D graphics focus on manipulating and rendering images in a two-dimensional space, 3D graphics introduce an additional dimension, offering a more realistic and immersive experience. The transition from 2D to 3D can be challenging, but it’s a natural extension of the principles you’ve already learned. You must understand 3D modeling, texturing, lighting, and rendering. These concepts are more complex as they involve dealing with 3D space, perspective, and more sophisticated algorithms for rendering.

Diving into software rendering in C++ is an excellent next step. A software renderer is a graphics engine that renders images without the aid of specialized graphics hardware. It relies on the CPU to process and render the graphics. Building a software renderer in C++ will deepen your understanding of graphics programming. You’ll learn about scanline rendering, z-buffering, texture mapping, and shading models. This process will also enhance your programming skills in C++, especially in areas like memory management, optimization, and understanding of low-level system architecture.

Simultaneously, exploring OpenGL will complement your journey. OpenGL is a cross-platform API used for rendering 2D and 3D vector graphics. It’s widely used in the industry and supports simple and complex graphics rendering. While software rendering gives you a fundamental understanding of how graphics are rendered, OpenGL provides a more practical approach to rendering graphics using the GPU. It’s efficient, faster, and supports many functions for generating advanced graphics. Learning OpenGL will expose you to GPU programming, shaders, and modern rendering techniques.

Turning mathematical notions into C++ code is crucial in graphics programming. Computer graphics is heavily based on mathematics, particularly linear algebra, geometry, and calculus. Concepts such as vectors, matrices, transformations, and interpolation are the backbone of graphics programming. To translate these concepts into C++, you must understand how to implement mathematical algorithms and data structures in code. For instance, implementing a vector class in C++ involves understanding the mathematical properties of vectors and then translating these properties into member functions and operators.

Starting with a pseudocode or a mathematical formula is often beneficial when dealing with complex mathematical notions. Breaking down the problem into smaller, manageable parts helps understand and code it effectively. For example, if you’re implementing a function for a Bezier curve, start by understanding the mathematical formula and then translate each part of the formula into a segment of the code. This approach makes the process more manageable and more systematic.

Debugging and optimization are critical skills as well. Translating mathematical concepts into code often leads to performance bottlenecks or unexpected results due to precision errors or inefficient algorithms. Profiling your code to identify and optimize slow sections is vital to development. Understanding algorithmic complexity and optimizing for speed and memory usage are essential skills in graphics programming.

Incorporating real-world physics can make your graphics more realistic and engaging. Physics simulations involving collision detection, particle systems, and fluid dynamics add more realism to graphics. While these concepts are mathematically intensive, they bring life to graphics. Implementing them in C++ requires a deep understanding of the physics concepts and how to execute them in code efficiently.

Learning concurrency is a pivotal aspect in the realm of high-performance computing. It is particularly relevant in computer graphics, where handling large volumes of data and complex computations simultaneously is commonplace. Concurrency involves executing multiple sequences of operations simultaneously, either through multi-threading or other parallel execution methods. In graphics programming, concurrency can significantly accelerate rendering processes and real-time computations. However, it introduces challenges such as synchronization, race conditions, and deadlocks. To effectively use conjunction, one must understand these challenges and master techniques like mutexes, semaphores, and lock-free algorithms. Big O notation is a valuable tool when measuring the performance improvements brought by concurrency. It helps evaluate algorithms’ efficiency, particularly in identifying bottlenecks in parallel code. By analyzing the time complexity of concurrent operations, you can optimize algorithms to achieve better performance and scalability.

Simultaneously, learning about Single Instruction, Multiple Data (SIMD), and loop unrolling can enhance code optimization, especially in graphics programming, where operations are often performed on significant data elements. SIMD allows a single instruction to process multiple data points simultaneously, which is highly efficient for operations common in graphics, such as matrix transformations or pixel manipulations. Implementing SIMD requires an understanding of processor architecture and how to leverage SIMD instruction sets like SSE or AVX in your code. On the other hand, loop unrolling is a technique used to increase the efficiency of loops by reducing the loop overhead and increasing the level of parallelism. By duplicating the code inside a loop, the number of iterations can be reduced, leading to faster execution times. SIMD and loop unrolling exploit the hardware capabilities to optimize performance. Combined with Big O analysis, these techniques allow for a thorough evaluation and enhancement of graphics code, leading to significant performance gains in computationally intensive tasks such as rendering and image processing.

Lastly, continually working on projects and building a portfolio is vital. Practical experience is invaluable in the field of computer graphics. Start with simple projects and gradually move to more complex ones. Participating in online communities and contributing to open-source projects can provide practical experience and peer feedback. This hands-on approach solidifies your understanding and prepares you for professional opportunities in computer graphics.

* * *

## Software Rendering in Three-D

Learning software rendering in C++ is an excellent endeavor for several compelling reasons, particularly for those interested in the fundamentals of computer graphics and low-level programming. Firstly, it provides a deep understanding of how graphics are rendered from the ground up. Unlike using high-level graphics APIs like OpenGL or DirectX, which abstract many of the underlying details, software rendering requires you to handle everything manually. This includes drawing pixels on the screen, implementing algorithms for line drawing, polygon filling, texture mapping, and handling lighting and shading calculations. By building a renderer from scratch, you gain a profound appreciation of the inner workings of graphics engines and the complexities involved in rendering images. This knowledge is invaluable for graphics programming and understanding the limitations and capabilities of hardware and software in rendering.

Secondly, programming a software renderer in C++ cultivates strong programming skills, particularly in areas like memory management, data structures, algorithm optimization, and understanding of system architecture. C++ is a language that grants close control over system resources and hardware, which is essential for performance-critical applications like graphics rendering. As you develop your renderer, you’ll encounter challenges that require a deep understanding of how the language works, from memory allocation and deallocation to the use of pointers and low-level data manipulation. These skills are highly transferable and beneficial in many areas of software development, especially in performance-intensive sectors.

Furthermore, learning software rendering aids in developing a problem-solving mindset and a detail-oriented approach. Software rendering involves complex mathematics and algorithms, requiring a precise and thoughtful implementation. Debugging and optimizing such code can be challenging, as minor errors can lead to significant issues in the output. This process cultivates patience, attention to detail, and systematic problem-solving skills. Additionally, the necessity to optimize for performance encourages innovative thinking and the development of efficient coding practices. This experience is invaluable in any programming field, as it teaches how to tackle complex problems systematically and efficiently.

Lastly, understanding software rendering is particularly beneficial for those interested in the evolution and future of graphics technology. With the advent of modern hardware and APIs, many principles of software rendering are being revisited and adapted. For example, understanding rasterization, a key concept in software rendering, is crucial for understanding the operation of modern GPUs. Similarly, as real-time ray tracing becomes more prevalent, the principles learned in software rendering, such as light and color calculations, become increasingly relevant. Additionally, with the continuous development of graphics technology, having a foundational understanding of these concepts provides a solid basis for adapting and innovating with new technologies as they emerge. In summary, learning software rendering in C++ is not just about understanding current practices; it’s about building a foundation to engage with the future of computer graphics.

A suggestion where to start: [Software rendering in C++](https://medium.com/@aminere/software-rendering-from-scratch-f60127a7cd58)

Source code on GitHub: [Platz](https://github.com/aminere/platz)

* * *

## Learn OpenGL Online

For several reasons, learning OpenGL, Vulkan, and Apple Metal2 alongside C++ is highly beneficial for graphics programmers. Firstly, these are among the industry’s most widely used graphics APIs, each serving different purposes and platforms. OpenGL is a well-established, cross-platform API that’s been the standard for 2D and 3D graphics programming for decades. It provides a vast range of functionalities for rendering sophisticated graphical content. It is supported on various hardware and operating systems, making it a versatile choice for many applications.

Conversely, Vulkan is a more recent API that offers higher performance and more direct control over GPU operations compared to OpenGL. It’s designed for modern, high-efficiency graphics and computing operations, making it particularly suitable for applications that require maximum performance. Apple Metal2 is designed for Apple’s hardware, providing optimized performance for iOS and macOS applications. Learning these APIs enhances a programmer’s versatility and employability, enabling them to work on various platforms and projects.

Secondly, mastering these APIs in conjunction with C++, a language known for its performance and control over hardware resources, significantly boosts a programmer’s ability to write efficient, high-performance graphics code. C++’s low-level capabilities complement the nature of these APIs, allowing for fine-tuned control over graphics rendering and efficient management of system resources. Understanding how to leverage C++ in conjunction with these APIs can lead to developing applications that fully utilize the hardware’s capabilities, whether for sophisticated 3D graphics, real-time simulations, or high-performance computing tasks.

Thirdly, each APIs offers unique learning experiences contribute to a well-rounded skill set. OpenGL provides a solid foundation in traditional graphics programming concepts applicable across many graphics APIs. Vulkan introduces programmers to a more explicit and detailed control of the graphics pipeline, offering insights into the workings of modern GPUs and the optimization of graphics rendering. Apple Metal2, with its focus on Apple’s ecosystem, offers a unique perspective on integrating graphics programming with Apple’s hardware and software, which is invaluable for developers focused on Apple platforms. Together, these APIs cover a broad spectrum of graphics programming techniques and concepts, ensuring that a programmer is well-equipped to tackle various challenges in the field.

Finally, the demand for sophisticated graphics is constantly growing in traditional areas like gaming and animation and emerging technologies like virtual reality, augmented reality, and scientific visualization. Expertise in these APIs means being at the forefront of creating immersive and high-quality graphical experiences. Moreover, the skills gained from working with these technologies are transferable to other areas of computing that require high-performance graphics processing. In essence, learning OpenGL, Vulkan, and Apple Metal2 with C++ is not just about mastering current technologies; it’s about positioning oneself at the cutting edge of technology, making it a wise investment for any ambitious graphics programmer.

Where to start? Here: [learnopengl.com](https://learnopengl.com/)

* * *

## From Paper to Code

For several compelling reasons, learning to translate mathematical notation into C++ is an essential skill for a graphics programmer. At the core of computer graphics lies a foundation of mathematics, including linear algebra, geometry, and calculus. These mathematical principles are used to model and manipulate 3D objects, control lighting, and shading, and simulate physical phenomena. Understanding how to convert these mathematical concepts into C++ code is crucial. It enables the programmer to implement rendering, animation, collision detection algorithms, and more. This translation requires a good grasp of mathematics and an understanding of how to effectively implement these concepts in a programming language known for its efficiency and control over hardware resources.

Secondly, translating mathematical notation into code enhances a programmer’s ability to create more efficient and optimized software. Graphics programming often involves complex calculations repeated millions of times per second. A deep understanding of the underlying mathematics allows a programmer to write code that is not just functionally correct but also efficient. By knowing how to implement these mathematical operations in C++, a programmer can optimize them to take full advantage of the hardware, like utilizing SIMD (Single Instruction, Multiple Data) instructions or parallel processing capabilities of modern CPUs and GPUs. This optimization is crucial in graphics programming, where performance can significantly impact the user experience.

Thirdly, this skill fosters innovation and creativity in problem-solving. Many challenges in graphics programming are unique and require custom solutions. By understanding how to translate complex mathematical ideas into practical code, programmers can devise novel algorithms and techniques that push the boundaries of what’s possible in computer graphics. This could range from developing advanced rendering techniques to creating realistic simulations of physical phenomena. The ability to innovate in this way is intellectually rewarding and highly valued in the industry.

Moreover, translating mathematical notation into C++ code encourages a more profound understanding of both disciplines. In its pure form, mathematics can be abstract and theoretical, while programming is practical and application-driven. Bridging these two worlds requires a deep understanding of both, and the translation process reinforces this understanding. It allows programmers to see the practical applications of mathematical concepts, which can lead to a deeper appreciation and understanding of mathematics.

In addition, this skill is crucial for collaboration and communication within interdisciplinary teams. Graphics programming often involves working with professionals from various fields, including artists, designers, and mathematicians. Understanding mathematical notation and translating it into code makes it easier to communicate complex ideas and collaborate effectively on projects. It ensures that the technical implementations align closely with the creative and conceptual visions of the team.

Finally, the ability to translate mathematical notation into C++ prepares a graphics programmer for the industry’s evolving landscape. As computer graphics technology advances, new mathematical models and techniques continually emerge. Programmers adept at translating these new ideas into executable code can stay at the forefront of the field, adapting to new technologies and methods. This adaptability is crucial in a constantly evolving industry where staying current with the latest developments is essential for success. In summary, learning to translate mathematical notation into C++ equips graphics programmers with a versatile and powerful skill set fundamental to success in this dynamic and exciting field.

* * *

#### Understanding the Product Symbol in Mathematical Notation

![](resources/math_01.png)

Figure 127

We often encounter the uppercase Pi symbol in mathematical notation, denoted as \Pi. However, it is crucial to understand that in this context, the symbol does not represent the Greek letter Pi but rather the concept of ‘Product’ in mathematics. This is a pivotal symbol used to denote the multiplication of a sequence of terms.

The LaTeX code for this symbol is \prod, where prod is an abbreviation for Product. The utilization of this symbol in mathematical expressions is analogous to a for-loop in programming languages. The terms located to the right of the product symbol \prod are those that are to be multiplied in the sequence.

Below the Product symbol, one typically encounters the notation `i=1.` This indicates the iterative multiplication process commences from the integer value `1,` with `i’` as the iterating variable. In each iteration, this variable `i` is multiplied by the product accumulated in the preceding steps.

Above the Product symbol, `n` is often placed. This `n` specifies the upper boundary of the iterative process, denoting the total number of iterations or the endpoint of the sequence.

This concept can be mathematically articulated in LaTeX as follows:

```
1 LaTeX:
2 \begin{align*}
3 factorial(n)=n!=\prod_{i=1}^n i
4 \end{align*}
```

Figure 128

Here, the expression describes the factorial of a number `n,` which is calculated as the product of all positive integers up to and including `n.` The factorial function holds significant importance in various branches of mathematics, including combinatorics and number theory, where it is used to compute permutations, combinations, and other related mathematical operations.

* * *

#### Understanding Factorials in Mathematics and C++

![](resources/math_02.png)

Figure 129

In mathematics, the concept of the factorial of a number `n,` commonly denoted as `n!,` is fundamental. The term `factorial` is articulated when referring to the exclamation mark in this context. The factorial of `n` is equivalent to the product of all positive integers up to `n.` This can be mathematically represented as the product, denoted by the uppercase Pi symbol \Pi, where the multiplication sequence commences from `1` and continues to `n.`

Translating this mathematical concept into a programming language such as C++, we can create a function to compute the factorial of a given number. Here is an illustrative example of such a function in C++:

```
 1 // From Paper to Code
 2 // Factorial
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \prod_{i=1}^5 i
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int factorial(int n) {
 9     int temp = 1;
10     for (int i = 1; i <= n; ++i) {
11         temp *= i;
12     }
13     return temp;
14 }
15 
16 int main() {
17     std::cout << "Factorial of 5 is: " << factorial(5) << std::endl;
18     std::cout << "This is the same as: 1*2*3*4*5, which is: " << 1*2*3*4*5 << std::e\
19 ndl;
20 }
```

Figure 130

* * *

#### Exploring the Concept of Summation in Mathematics and Its Implementation in C++

![](resources/math_03.png)

Figure 131

In the example, we encounter a mathematical expression featuring a prominent sigma symbol surrounded by various notations. This symbol represents the concept of `summation` in mathematics. The equation involves the constant `e,` a fundamental mathematical constant known for its applications in calculus and complex analysis.

The value of `e` can be approximated by employing the summation process indicated in the equation. This involves summing the inverse of the factorial of `n,` starting from `n = 0` and theoretically continuing to infinity.

The LaTeX notation for this summation is as follows:

```
1 \begin{align*}
2 e = \sum_{n=0}^{\infty} \frac{1}{n!}
3 \end{align*}
```

Figure 132

In practice, computing this summation to infinity is not feasible. Therefore, an approximation approach is adopted by defining a finite number of iterations, which in this case is chosen to be 100\. It is also important to note that division by zero is undefined in mathematics, necessitating a conditional check in the computation to avoid such scenarios.

The following C++ code snippet demonstrates how to approximate the value of `e` using the summation method:

```
 1 // From Paper to Code
 2 // Factorial
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: e = \sum_{n=0}^{\infty} \frac{1}{n!}
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int factorial(int n) {
 9     int temp = 1;
10     for (int i = 1; i <= n; ++i) {
11         temp *= i;
12     }
13     return temp;
14 }
15 
16 double e() {
17     double temp = 0.0;
18     int temp2 = 0;
19     for (int n = 0; n < 100; ++n) { // Approximating infinity with 100 iterations.
20         temp2 = factorial(n);
21         if (temp2 != 0) { // Ensuring division by zero does not occur.
22             temp += 1.0 / temp2;
23         }
24     }
25     return temp;
26 }
27 
28 int main() {
29     std::cout << "e(): " << e() << std::endl;
30     std::cout << "Instead of running: 1.0/(factorial(0))+1.0/(factorial(1))+1.0/(fac\
31 torial(2))+1.0/(factorial(3))..." << std::endl;
32 }
```

Figure 133

We run the code and see that `e` equals `2.71828.`

* * *

#### Calculating the Average of a Number Collection in Mathematics and C++

![](resources/math_04.png)

Figure 134

In this example, we examine calculating the average of a set of numbers. Let `X` be defined as a collection of numbers, represented as `X = \{x1,x2….xn\};.` Here, `X` can comprise any number, and they can occupy any position within the collection. The average of `X,` denoted as `avg(X),` is computed as the sum of all elements in `X` divided by the number of elements in `X` (the length of the collection).

The mathematical representation of this concept uses the notation `|X|` to indicate the length or cardinality of the collection `X.` The average is then calculated using the formula:

```
1 LaTeX:
2 \begin{align*}
3 X = \{X_{1},X_{2},…,X_{n} \};
4 avg(X) = \frac{1}{|x|} \sum_{i\epsilon\{1,2..n\}} x_{i}
5 \end{align*}
```

Figure 135

In this formula, the summation runs from `1` to `n,` where `n` is the number of elements in `X,` and `i’` is the index to access each element in the collection.

In practical terms, the collection `X` can be an array of numbers or any data structure that stores a collection of values. `X_i` represents each element of the collection indexed by `i.`

To implement this mathematical concept in C++, we can write a function to compute the average of a collection of numbers using a `std::vector<double>.` The following C++ code demonstrates this approach:

```
 1 // From Paper to Code
 2 // Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: X = \{X_{1}, X_{2}, ..., X_{n} \};
 5 // LaTeX: avg(X) = \frac{1}{|X|} \sum_{i \in \{1,2..n\}} X_i
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <iostream>
 8 #include <vector>
 9 
10 double avg(std::vector<double> &X) {
11     double temp = 0.0;
12     for (int i = 0; i < X.size(); ++i) {
13         temp += X[i];
14     }
15     temp /= X.size();
16     return temp;
17 }
18 
19 int main() {
20     std::vector<double> grades = {3.0, 1.0, 4.0};
21     std::cout << "avg(grades) = " << avg(grades) << std::endl;
22     std::cout << "Which is the same as: (3.0 + 1.0 + 4.0) / 3, which is: " << (3.0 +\
23  1.0 + 4.0) / 3 << std::endl;
24 }
```

Figure 136

When running the code, the result is an average grade of `2.66667.`

* * *

#### Understanding the Notation ‘x e X’ in Set Theory and Its Implementation in Code

![](resources/math_05.png)

Figure 137

The notation `x e X,` frequently encountered in set theory, signifies that the element represented by the lowercase `x` is a member of the set denoted by the uppercase `X.` This mathematical concept asserts that each instance of `x` is drawn from the elements that constitute the set `X.`

To elucidate, when we state `x e X,` we are indicating that `x` is one of the elements within the collection `X.` In mathematical terms, `X` is referred to as a set, and it can consist of various elements, such as numbers, characters, or even other sets. The symbol `e` is a fundamental element of set notation and is read as `is an element of` or `belongs to.`

This concept forms the basis of set theory, a branch of mathematical logic that studies collections of objects, referred to as sets, and is foundational in various areas of mathematics and computer science.

This concept can be implemented in computer programming, particularly when dealing with arrays, lists, or other data structures, to check if a particular value exists within a given collection. Here is a simple example in C++ that demonstrates checking if an element is part of a collection:

```
 1 // From Paper to Code
 2 // Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: X = \{X_{1},X_{2},...,X_{n} \};
 5 // LaTeX: avg(X) = \frac{1}{|x|} \sum_{x \epsilon X} x
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <iostream>
 8 #include <vector>
 9 
10 double avg(std::vector<double> &X)
11 {
12     double temp=0.0;
13     for (auto& x : X) // element x from X (xeX)
14     {
15         temp = temp + x;
16     }
17     temp = temp*1.0/X.size();
18     return temp;
19 }
20 
21 int main()
22 {
23     std::vector<double> grades = {3.0, 1.0, 4.0};
24     std::cout << "avg(grades) = " << avg(grades) << std::endl;
25     std::cout << "Which is the same as: (3.0+1.0+4.0)/3, which is: " << (3.0+1.0+4.0\
26 )/3 << std::endl;
27 }
```

Figure 138

* * *

#### Computing Variance Using Nested Summation in Mathematics and C++

![](resources/math_06.png)

Figure 139

In this section, we delve into variance, denoted as `var,` a fundamental statistical measure that quantifies the spread or dispersion of data points. The variance calculation uses two summation symbols, represented by sigma (\Sigma), symbolizing a nested loop structure in computational terms. This nested loop methodology is akin to executing a loop within another loop, a common practice in various programming languages for handling multi-dimensional data.

The mathematical formulation for the variance of a set `X = {X_1, X_2, …, X_n` is represented:

```
1 LaTeX:
2 \begin{align*}
3 X = \{X_{1},X_{2},…,X_{n} \};
4 var(X) = \frac{1}{|x|²} \sum_{x \epsilon X} \sum_{x \epsilon X} \frac{1}{2} (i — j)²
5 \end{align*}
```

Figure 140

In this formula, `|X|` denotes the number of elements in the set `X,` and the double summation iterates over each pair of elements in `X,` calculating the squared difference between each pair, divided by `2.` This method effectively captures the variance of the dataset, reflecting the average degree to which each point differs from the others.

To implement this mathematical concept in a programming language like C++, we use nested loops to iterate over all pairs of elements in a data collection. The following C++ code demonstrates the computation of variance for a given vector of data:

```
 1 // From Paper to Code
 2 // Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: X = \{X_{1}, X_{2}, ..., X_{n} \};
 5 // LaTeX: var(X) = \frac{1}{|X|^2} \sum_{x \in X} \sum_{x \in X} \frac{1}{2} (i - j)\
 6 ^2
 7 // Test LaTeX: https://quicklatex.com/
 8 #include <iostream>
 9 #include <vector>
10 #include <cmath>
11 
12 double var(std::vector<double> &X) {
13     double temp = 0.0;
14     for (auto i: X) {
15         for (auto j: X) {
16             temp += (1.0 / 2.0) * pow((i - j), 2);
17         }
18     }
19     temp *= 1.0 / pow(X.size(), 2);
20     return temp;
21 }
22 
23 int main() {
24     std::vector<double> grades = {3.0, 1.0, 4.0};
25     std::cout << "var(grades) = " << var(grades) << std::endl;
26 }
```

Figure 141

Which gives us the variance: `1.55556`

* * *

### Square Root

`√ — always` means the positive square root. A square root of a number is a value that gives the number when multiplied by itself.

Example: `4 × 4 = 16,` so a square root of `16` is `4.` Note that `(−4) × (−4) = 16` too, so `−4` is also a square root of `16.`

Example: `√36 = 6`

Cube Root: The cube root of a number is a unique value that gives that number when used in multiplication three times.

Example: `3 × 3 × 3 = 27`

```
1 LaTeX: \sqrt{n}
2 LaTeX: \sqrt{16}
3 LaTeX: \sqrt[3]{n}
4 LaTeX: \sqrt[3]{27}
```

Figure 142

![](resources/math_07.png)

Figure 143

In code:

```
 1 // From Paper to Code
 2 // Square Root
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sqrt{16}
 5 // LaTeX: \sqrt[3]{27}
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <iostream>
 8 #include <cmath>
 9 
10 int main() {
11     std::cout << "Square Root of 16 equals: " << sqrt(16) << std::endl;
12     std::cout << "Cubic Root of 27 equals: " << cbrt(27) << std::endl;
13 }
```

Figure 144

* * *

### Complex Numbers

A `Complex Number` combines a `Real Number` and an `Imaginary Number.`

Example: `a + bi`

Example `a` plus `b` `i.` `a` is the real part. `b` is the imaginary part. The `unit` imaginary number (like `1` for Real Numbers) is `i,` which is the square root of minus one.

`i² = −1`

When we square `i, ' we get −1.`

Example: `7 + 3i`

For instance, this example: seven plus `3` `i.` We keep that little `i` there to remind us to multiply by the square root of minus one.

Comment: The absolute value of a complex number, `a + bi` (also called the modulus), is defined as the distance between the origin `(0,0)` and the point `(a,b)` in the complex plane.

Comment: The argument of a complex number is usually given in radians in the range `−𝜋` to `𝜋.`

Latex: `7 + 3i`

![](resources/math_08.png)

Figure 145

In code:

```
 1 // From Paper to Code
 2 // Complex Numbers
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: 7 + 3i
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <complex>
 8 
 9 int main() {
10     // defines the complex number: (7.0 + 3.0i)
11     std::complex<double> mycomplex (7.0, 3.0);
12 
13     // prints the real part using the real function
14     std::cout << "Real part: " << real(mycomplex) << std::endl;
15     std::cout << "Imaginary part: " << imag(mycomplex) << std::endl;
16 
17     // prints the absolute value of the complex number
18     std::cout << "The absolute value of " << mycomplex << " is: ";
19     std::cout << abs(mycomplex) << std::endl;
20 
21     // prints the argument of the complex number
22     std::cout << "The argument of " << mycomplex << " is: ";
23     std::cout << arg(mycomplex) << std::endl;
24 }
```

Figure 146

* * *

### Dot and Cross Product

The space dot · and cross symbols × have different uses depending on context. They might seem obvious, but it’s essential to understand the subtle differences before we continue into other sections.

#### Scalar Multiplication

```
1 5 · 4 = 5 × 4
```

Figure 147

Both symbols can represent simple multiplication of scalars. These are equivalent. Five space dot four is the same as five cross four.

```
1 LaTeX: 5 \cdot 4 = 5 \times 4
2 
3 int result = 5 * 4;// In C++.
```

Figure 148

But in programming languages, we tend to use asterisk for multiplication.

```
1 3kj
```

Figure 149

Often, the multiplication sign is only used to avoid ambiguity. Here, we can omit it entirely.

```
1 int result = 3 * k * j;// In C++.
```

Figure 150

If these variables represent scalars, the code would be this.

#### Vector Multiplication

To denote the multiplication of one vector with a scalar or element-wise multiplication of a vector with another vector, we typically do not use the space dot · or cross symbols ×. These have different meanings in linear algebra.

Let’s take our earlier example but apply it to vectors. You might see an open dot ○ to represent the Hadamard product for element-wise vector multiplication. The Hadamard product is a binary operation that takes two matrices of the exact dimensions and produces another matrix of the same dimension as the operands, where each element i, j is the product of elements i, j of the original two matrices. It is to be distinguished from the more common matrix product. It is attributed to and named after either French mathematician Jacques Hadamard or German mathematician Issai Schur.

![](resources/math_09.png)

Figure 151

```
1 LaTeX: 3k \circ j
```

Figure 152

In other instances, the author might explicitly define a different notation, such as a circled dot ⊙ or a filled circle ●.

```
 1 // From Paper to Code
 2 // Dot and Cross - vector multiplication
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: 3k \circ j
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8 
 9 void multiply(std::vector<int> &a, std::vector<int> &b, std::vector<int> &c)
10 {
11     if (a.size() == b.size())
12     {
13         for (int i=0;i<a.size();++i) {
14             c.push_back(a[i] * b[i]);   
15         }
16     }
17 }
18 
19 void multiplyScalar(std::vector<int> &a, int s, std::vector<int> &c)
20 {
21     for (int i=0;i<a.size();++i) {
22         c.push_back(a[i] * s);   
23     }
24 }
25 
26 int main() {
27     int s = 3;
28     std::vector<int> k = {2 , 7 , 4 , 5};
29     std::vector<int> j = {2 , 7 , 4 , 5};
30     std::vector<int> tmp;
31     std::vector<int> result;
32 
33     multiply(k, j, tmp);
34     multiplyScalar(tmp, s, result);
35 
36     std::cout << "Scalar: " << s << '\n' << "k: ";
37     for (auto const& e : std::as_const(k)) {
38         std::cout << e << " ";
39     }
40     std::cout << '\n' << "j: ";
41     for (auto const& e : std::as_const(j)) {
42         std::cout << e << " ";
43     }
44     std::cout << '\n' << "Multiply(tmp): ";
45     for (auto const& e : std::as_const(tmp)) {
46         std::cout << e << " ";
47     }
48     std::cout << '\n' << "Scaler Multiplication(result): ";
49     for (auto const& e : std::as_const(result)) {
50         std::cout << e << " ";
51     }
52     std::cout << '\n';
53 }
```

Figure 153

#### Dot Product

![](resources/math_10.png)

Figure 154

The space dot · symbol can denote the dot product of two vectors. Sometimes, this is called the scalar product since it evaluates to a scalar.

```
 1 // From Paper to Code
 2 // Dot and Cross - Dot Product
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k\cdot j
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8 
 9 double dot(std::vector<double> &a, std::vector<double> &b)
10 {
11     double tmp=0.0;
12 
13     if (a.size() == b.size())
14     {
15         for (int i=0;i<a.size();++i) {
16             tmp = tmp + (a[i] * b[i]);   
17         }
18     }
19     
20     return tmp;
21 }
22 
23 int main() {
24     std::vector<double> k = {0.0 , 1.0 , 0.0};
25     std::vector<double> j = {1.0 , 0.0 , 0.0};
26 
27     double d = dot(k, j);
28 
29     if (d == 0.0)
30     {
31         std::cout << "Vectors are perpendicular to each other." << std::endl;
32     }
33 }
```

Figure 155

```
1 LaTeX: k \cdot j
```

Figure 156

Dot Product is a common feature of linear algebra, and with a 3D vector, it might in C++ look like this. Here, we have a function called dot that returns a double. The function takes two vectors, a and b, as input. The result is calculated by multiplying each element at the same index between vectors a and b. The result of the multiplication gets added to tmp each time.

The result `0.0` tells us our vectors are perpendicular.

#### Cross Product

![](resources/math_11.png)

Figure 157

This is an example of a × cross-product of two vectors.

```
1 LaTeX: k \times j
```

Figure 158

```
 1 // From Paper to Code
 2 // Dot and Cross - Cross Product
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k \times j
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <tuple>
 8 
 9 std::tuple<double,double,double> cross(std::tuple<double,double,double> &a, std::tup\
10 le<double,double,double> &b)
11 {
12     double ax=0.0,ay=0.0,az=0.0;
13     double bx=0.0,by=0.0,bz=0.0;
14     double rx=0.0,ry=0.0,rz=0.0;
15 
16     std::tie (ax, ay, az) = a; // unpack elements
17     std::tie (bx, by, bz) = b; // unpack elements
18 
19     rx = ay * bz - az * by;
20     ry = az * bx - ax * bz;
21     rz = ax * by - ay * bx;
22 
23     return std::make_tuple(rx, ry, rz);
24 }
25 
26 int main() {
27     std::tuple<double,double,double> k(0.0 , 1.0 , 0.0);
28     std::tuple<double,double,double> j(1.0 , 0.0 , 0.0);
29 
30     std::tuple<double,double,double> result = cross(k, j);
31 
32     std::cout << "Result = [ " << std::get<0>(result) << ", " << std::get<1>(result)\
33  << ", " << std::get<2>(result) << " ]" << std::endl;
34 }
```

Figure 159

The function takes the reference of 2 tuples as input and returns a tuple with the answer. Result `x` is calculated by multiplying a `y` with `b` `z` and multiplying `a` `z` with `b` `y.` Then subtract the second multiplication from the first. Result `y` is calculated by multiplying `a` `z` with `b` `x` and multiplying `a` `x` with `b` `z.` Then subtract the second multiplication from the first. Result `z` is calculated by multiplying `a` `x` with `b` `y` and multiplying `a` `y` with `b` `x.` Then subtract the second multiplication from the first.

Result = `[ 0, 0, -1 ]`

* * *

### Sigma - Sum of Sequence

The big Greek Sigma is for Summation. In other words, I am summing up some numbers.

```
1 LaTeX: \sum_{i=1}^{100} i
```

Figure 160

![](resources/math_12.png)

Figure 161

What we get from latex is this. Here, `i=1` says to start at `1` and end at the number above the Sigma, `100.` These are the `lower` and `upper bounds,` respectively. The `i` to the right of the Sigma tells us what we are summing.

In C++:

```
 1 // From Paper to Code
 2 // Sigma - Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{100} i
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int sum=0;
10     for (int i=1;i<=100;i++)
11     {
12         sum += i;
13     }
14 
15     std::cout << "Sum = " << sum << std::endl;
16 }
```

Figure 162

Here we have two variables, `sum` and `i.` The sum is initialized to `zero.` `i` is initialized to `1` in a for loop that counts up to `100.` Within the for loop, we add `i` to the `sum.`

The result (`sum)` we get when running the code is: `5050.`

![](resources/math_13.png)

Figure 163

```
1 LaTeX: \sum_{i=1}^{100} (2i + 1)
```

Figure 164

In C++:

```
 1 // From Paper to Code
 2 // Sigma - Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{100} (2i + 1)
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int sum=0;
10     for (int i=1;i<=100;i++)
11     {
12         sum += (2 * i + 1);
13     }
14 
15     std::cout << "Sum = " << sum << std::endl;
16 }
```

Figure 165

The calculation’s result (`sum)` is: `10200.`

The notation can be nested, much like nesting a for loop. You should evaluate the right-most sigma first unless the author has enclosed them in parentheses to alter the order. However, in the following case, since we are dealing with finite sums, the order does not matter.

![](resources/math_14.png)

Figure 166

```
1 LaTeX: \sum_{i=1}^{2} \sum_{j=4}^{6} (3ij)
```

Figure 167

In C++:

```
 1 // From Paper to Code
 2 // Sigma - Summation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \sum_{i=1}^{2} \sum_{j=4}^{6} (3ij)
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int sum=0;
10     for (int i = 1; i <= 2; i++) {
11         for (int j = 4; j <= 6; j++) {
12             sum += (3 * i * j);
13         }
14     }
15 
16     std::cout << "Sum = " << sum << std::endl;
17 }
```

Figure 168

The result (`sum)` is: `135`

* * *

### Capital Pi — Product of Sequences

The capital Pi or “Big Pi” is very similar to Sigma, except we use multiplication to find the product of a sequence of values.

![](resources/math_15.png)

Figure 169

```
1 LaTeX: \prod_{i=1}^{6} i
```

Figure 170

In C++:

```
 1 // From Paper to Code
 2 // Capital Pi - Product
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \prod_{i=1}^{6} i
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int prod = 1;
10     for (int i = 1; i <= 6; i++) {
11         prod *= i;
12     }
13 
14     std::cout << "Product = " << prod << std::endl;
15 }
```

Figure 171

We have two variables called: `prod` and `i.` `Prod` is initialized with a `1.` `i` is initialized with a `1.` The for-loop count is up to `6.` Within the for loop, we multiply `prod` with `i` and store the result as `prod.`

The result when running the code is: `720`

* * *

### Pipes

Pipe symbols ||, known as bars, can mean different things depending on the context. We are going through three common uses: absolute value, Euclidean norm, and determinant.

These three features all describe the length of an object.

#### Absolute Value

absolute value or modulus of a real number 3 is 3, and the absolute value of −3 is also 3\. A number’s absolute value may be considered its distance from zero.

Generalizations of the absolute value for real numbers occur in various mathematical settings. For example, a total value is also defined for complex numbers, quaternions, ordered rings, fields, and vector spaces. The absolute value is closely related to the notions of magnitude, distance, and norm in various mathematical and physical contexts.

![](resources/math_16.png)

Figure 172

```
1 LaTeX: |x|
```

Figure 173

In C++:

```
 1 // From Paper to Code
 2 // Pipes - Absolute Value
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: |x|
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int x = -5;
10     int result = std::abs(x);
11 
12     std::cout << "Absolut Value of -5 = " << result << std::endl;
13 }
```

Figure 174

In this example, we want the `absolute value` of `x` that is `-5.` With the standard function `abs(),` we get the result `5.` As the distance from `zero` is `5.`

#### Euclidean norm

For a vector `v,` bar bar v bar bar is the Euclidean norm of `v.` It is also referred to as the `magnitude` or `length` of a vector. Often, this is represented by double bars to avoid ambiguity with the absolute value notation, but sometimes, you may see it with single bars.

![](resources/math_17.png)

Figure 175

```
1 LaTeX: ||v||
```

Figure 176

In C++:

```
 1 // From Paper to Code
 2 // Pipes - Euclidean norm
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: ||v||
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <tuple>
 8 #include <cmath>
 9 
10 double length(std::tuple<double,double,double> &vec)
11 {
12     double x=0.0,y=0.0,z=0.0;
13     std::tie (x, y, z) = vec;
14     return sqrt(x * x + y * y + z * z);
15 }
16 
17 int main() {
18     std::tuple<double,double,double> v(0.0, 4.0, -3.0);
19     std::cout << "The length of vector = " << length(v) << std::endl;
20 }
```

Figure 177

We include a tuple to hold the `x y z` values. We also include cmath for square root. We have a function called length that returns a double. Function length refers to a tuple called `vec` as input. We unpack `vec` into `x y z` variables of the type double. We then calculate the length by first multiplying. `x` * `x.` `y` * `y.` `z` * `z.` We add the result of the multiplications together. Then, we get the square root of the result and return it. The `x y z` used here are: `0.0 4.0` and `-3.0.`

The result of the calculation gives us that the length of the vector is `5`

#### Determinant

For a matrix A, bar A bar means the determinant of matrix A. The determinant is a scalar value that is a function of the entries of a square matrix. It allows for the characterization of some matrix properties and the linear map represented by the matrix.

![](resources/math_18.png)

Figure 178

```
1 LaTeX: |A|
```

Figure 179

In C++:

```
 1 // From Paper to Code
 2 // Pipes - Determinant
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX:  |A|
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8 
 9 double determinant(std::vector<std::vector<double>> &a)
10 {
11     double c, r=1;
12     int n=2;
13     for(int i = 0; i < n; i++) {
14         for(int k = i+1; k < n; k++) {
15             c = a[k][i] / a[i][i];
16             for(int j = i; j < n; j++)
17                 a[k][j]=a[k][j] - c*a[i][j];
18         }
19     }
20     for (int i = 0; i < n; i++)
21     {
22         r*=a[i][i];
23     }
24     return r;
25 }
26 
27 int main() {
28     std::vector<std::vector<double>> matrix = { {1.0 , 0.0} , {0.0 , 1.0} };
29     double det = determinant(matrix);
30     std::cout << "Determinant(Matrix) = " << det << std::endl;
31 }
```

Figure 180

We include a vector header for the vector within a vector of doubles called matrix, for holding our 2 by 2 matrix. The determinant function returns a double and refers to a vector within a vector of doubles.

By running this example, we get that the determinant of this vector is equal to `1`

* * *

### Hat — Unit Vector

The `hat` symbol above a character represents a unit vector in geometry. In this example, it’s the unit vector of a.

![](resources/math_19.png)

Figure 181

```
1 LaTeX: \hat{a}
```

Figure 182

In Cartesian space, a unit vector is typically of length equal to: `1.` That means each part of the vector will be in the range of `minus 1.0` to `1.0.` In the following C++ code, we normalize a 3D vector into a unit vector.

In C++:

```
 1 // From Paper to Code
 2 // Hat
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \hat{a}
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <tuple>
 8 #include <cmath>
 9 
10 std::tuple<double,double,double> normalize(std::tuple<double,double,double> &vec)
11 {
12     double x=0.0,y=0.0,z=0.0;
13     std::tie (x, y, z) = vec; // Unpack elements.
14 
15     double squaredLength = x * x + y * y + z * z;
16 
17     if (squaredLength > 0.0)
18     {
19         double length = sqrt(squaredLength);
20         return std::make_tuple( (x / length), (y / length), (z / length));
21     }
22     return vec;
23 }
24 
25 int main() {
26     std::tuple<double,double,double> a( 0.0, 4.0, -3.0 );
27     std::tuple<double,double,double> result=normalize(a);
28     std::cout << "Normalized 3D vector = [ " << std::get<0>(result) << ", " << std::\
29 get<1>(result) << ", " << std::get<2>(result) << " ]" << std::endl;
30 }
```

Figure 183

We include a tuple to hold the `x y z` vector. We include cmath for square root. The normalize function returns a tuple and takes a reference of a tuple as input. We unpack the tuple into `x y z` variables. We calculate the square length. We check whether the squared length is larger than `0.0.` If so, we calculate length by getting the square root of the variable square length and return `x y z` divided each with length and packed into a tuple. Lastly, we return the tuple.

Normalized 3D vector = `[ 0, 0.8, -0.6 ]`

* * *

### ”element of”

In set theory, the `element of` symbol `is a member of` and `has member` can be used to describe whether something is an `element of a set.`

For example, this. Here we have a set of numbers A: `3,` `9,` and `14.` And we are saying `3` is an `element of` that set.

![](resources/math_20.png)

Figure 184

```
1 LaTeX: A=\left \{ 3,9,14 \right \}, 3 \in A
```

Figure 185

In C++:

```
 1 // From Paper to Code
 2 // Element of
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: A=\left \{ 3,9,14  \right \}, 3 \in A
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8 #include <algorithm>
 9 
10 bool has(std::vector<int> &v, int e)
11 {
12     if (std::find(v.begin(), v.end(), e) != v.end())
13     {
14         return true;
15     }
16     return false;
17 }
18 
19 int main() {
20     std::vector<int> A = { 3, 9, 14 };
21     if (has(A,3))
22     {
23         std::cout << "Element found" << std::endl;
24     } else {
25         std::cout << "Element not found" << std::endl;
26     }
27 }
```

Figure 186

We include the vector header as we use a vector to hold our numbers. In this case, the numbers are: `3, 9` and `14.` We also include an algorithm vector for finding the element we seek. The function returns a boolean (true if the element is part of the number set. Else false). In this case, we get that the element is found.

The backward member is the same, but the order changes.

![](resources/math_21.png)

Figure 187

You can also use the `not an element of` symbols.

![](resources/math_22.png)

Figure 188

* * *

### Common Number Sets

![](resources/math_23.png)

Figure 189

Here, we have a few common sets and their symbols placed before them.

[R]eal Numbers The large R describes the set of real numbers. These include integers, as well as rational and irrational numbers. Real numbers are also finite, as in not infinite.

[Q] Rational Numbers Rational numbers are real numbers that can be expressed as a fraction or ratio, like three-fifths. Rational numbers cannot have zero as a denominator.

This also means that all integers are rational numbers since the denominator can be expressed as `1`

An irrational number, on the other hand, cannot be expressed as a ratio, like Pi, that is: `3.14159265359`

[Z] Integers An integer or a real number with no fractional part can be positive or negative.

[N]]atural Numbers A natural number is a positive and non-negative integer. Depending on the context and field of study, the set may or may not include zero.

[C]omplex Numbers A complex number combines real and imaginary numbers, viewed as coordinates in the 2D plane.

* * *

### Function

Functions are fundamental features of mathematics, and the concept is easy to translate into code.

A function relates an input to an output value. This is a function.

![](resources/math_24.png)

Figure 190

We can give this function a name. Commonly, we use `f` to describe a function, but it could be named A or anything else.

![](resources/math_25.png)

Figure 191

```
1 LaTeX: f\left (x \right ) = x^{2}
```

Figure 192

In C++:

```
 1 // From Paper to Code
 2 // Function
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: f\left (x \right) = x^{2}
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cmath>
 8 
 9 int square(int x)
10 {
11     return pow(x,2);
12 }
13 
14 int main() {
15     std::cout << "10^2 = " << square(10) << std::endl;
16 }
```

Figure 193

Running the code, we get that `10` squared is: `100`

Sometimes, a function is not named; instead, the output is written. Here, `x` is the input, the relationship is squaring, and `y` is the output.

![](resources/math_26.png)

Figure 194

Functions can also have multiple parameters, like in a programming language. These are known as arguments in mathematics, and the number of arguments a function takes is known as the “arity” of the function.

![](resources/math_27.png)

Figure 195

In C++:

```
 1 // From Paper to Code
 2 // Function
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: f(x,y) = \sqrt{x^2 + y^2}
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cmath>
 8 
 9 int length(int x, int y)
10 {
11     return sqrt(x * x + y * y);
12 }
13 
14 int main() {
15     std::cout << "length(4, 5) = " << length(4, 5) << std::endl;
16 }
```

Figure 196

Here, we have a function called length that takes two inputs, two parameters, or two arguments (whatever you wish to call it). It’s `x` and `y` in this case. Both are integers.

Running the code gives us that the length is `6` if `x` equals `4` and `y` equals `5.`

#### Piecewise function

Some functions will use different relationships depending on the input value: `x`

The function `f` chooses between two `sub-functions` depending on the input value. This is very similar to if or else in code. The right side conditions are often written as `for x is less than 0` or `if x equals 0.` If the condition is true, the function to the left is used.

In piecewise functions, `otherwise` and `elsewhere` are analogous to the else statement in code.

![](resources/math_28.png)

Figure 197

In C++:

```
 1 // From Paper to Code
 2 // Piecewise Function
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: f(x)= 
 5 // \begin{cases}
 6 //     \frac{x^2-x}{x},& \text{if } x\geq 1\\
 7 //     0, & \text{otherwise}
 8 // \end{cases} 
 9 // Test LaTeX: https://quicklatex.com/
10 #include <iostream>
11 #include <cmath>
12 
13 int f(int x)
14 {
15     if (x >= 1) {
16         return (pow(x, 2) - x) / x;
17     }
18 
19     return 0;
20 }
21 
22 int main() {
23     std::cout << "f(5) = " << f(5) << std::endl;
24 }
```

Figure 198

Here, we can see that the function `f` has an if statement, checking if `x` is greater or equal to zero, then performing the equation and returning the result. Else, return zero.

Running the code with `x equal to five` gives us a `4.`

#### Common functions

Some function names are ubiquitous in mathematics. For a programmer, these might be analogous to functions `built-in` to the language. One such example is the `sgn` function. This is the `signum` or `sign` function.

Here, we use piecewise function notation to describe it.

![](resources/math_29.png)

Figure 199

In C++:

```
 1 // From Paper to Code
 2 // Common Function
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \begin{cases}
 5 //     -1& \text{if } x < 0\\
 6 //     0, & \text{if } {x = 0}\\
 7 //     1, & \text{if } x > 0\\
 8 // \end{cases}
 9 // Test LaTeX: https://quicklatex.com/
10 #include <iostream>
11 
12 int sgn(int x)
13 {
14     if (x < 0) return -1;
15     if (x > 0) return 1;
16     return 0;
17 }
18 
19 int main() {
20     std::cout << "sgn(-5) = " << sgn(-5) << std::endl;
21 }
```

Figure 200

Running the code, we get `minus 1,` as `minus 5` is less than zero. Other common functions are: `sin,` `cos,` `tan.`

#### Function notation

In some literature, functions may be defined with more explicit notation.

![](resources/math_30.png)

Figure 201

It might also be written like this. The arrow here with a tail typically means `maps to,` as in `x` maps to `x squared.`

![](resources/math_31.png)

Figure 202

A function’s domain and codomain are similar to its input and output types. Here’s another example, using our earlier sgn function, which outputs an integer.

![](resources/math_32.png)

Figure 203

The arrow here (without a tail) maps one set to another.

![](resources/math_33.png)

Figure 204

* * *

### Prime

The prime symbol (’) is often used in variable names to describe similar things without giving it a different name altogether. It can describe the “next value” after some transformation.

For example, if we take a 2D point x y and rotate it, you might name the result x prime, y prime. Or, the transpose of matrix M might be named M prime.

We typically assign the variable a more descriptive name in code, like transformed Position.

For a mathematical function, the prime symbol often describes the derivative of that function. Let’s take this as our earlier function.

![](resources/math_34.png)

Figure 205

Its derivative could be written with a prime symbol.

![](resources/math_35.png)

Figure 206

In C++:

```
 1 // From Paper to Code
 2 // Prime
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: f'(x) = 2x
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cmath>
 8 
 9 int f(int x)
10 {
11     return pow(x, 2);
12 }
13 
14 int fPrime(int x)
15 {
16     return 2 * x;
17 }
18 
19 int main() {
20     std::cout << "f(5) = " << f(5) << " | fPrime(5) = " << fPrime(5) << std::endl;
21 }
```

Figure 207

Here, we can see both functions as: `f.` And the functions derivative as: `f prime.`

This gives us `25` as the answer to `5 squared` and that `f prime` of `5` is equal to: `10`

Multiple prime symbols can be used to describe the second derivative and third derivative. After this, authors typically express higher orders with roman numerals or superscript numbers.

f’’ f’’’ fIV f(n)

* * *

### Floor & Ceiling

The special brackets floor x floor and ceil x ceil represent the floor and ceil functions, respectively. Floor means the nearest integer not greater than the given value. Ceil means the nearest integer not less than the given value.

![](resources/math_36.png)

Figure 208

In C++:

```
 1 // From Paper to Code
 2 // Floor & Ceiling
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \lfloor x \rfloor
 5 // LaTeX: \lceil x \rceil 
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <iostream>
 8 #include <cmath>
 9 
10 int main() {
11     // Example of floor()
12     std::cout << "Example of floor():" << '\n' << std::fixed
13         << "floor(+2.7) = " << std::floor(+2.7) << '\n'
14         << "floor(-2.7) = " << std::floor(-2.7) << '\n'
15         << "floor(-0.0) = " << std::floor(-0.0) << '\n'
16         << "floor(-Inf) = " << std::floor(-INFINITY) << '\n';
17 
18     // Example of ceil()
19     std::cout << '\n' << "Example of ceil():" << '\n' << std::fixed
20         << "ceil(+2.4) = " << std::ceil(+2.4) << '\n'
21         << "ceil(-2.4) = " << std::ceil(-2.4) << '\n'
22         << "ceil(-0.0) = " << std::ceil(-0.0) << '\n'
23         << "ceil(-Inf) = " << std::ceil(-INFINITY) << '\n';
24 }
```

Figure 209

Both floor and ceil are part of the standard library header cmath. When the two symbols are mixed, it typically represents a function that rounds to the nearest integer.

![](resources/math_37.png)

Figure 210

In C++:

```
 1 // From Paper to Code
 2 // Floor & Ceiling
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: \lfloor x \rfloor
 5 // LaTeX: round(x) =  \lfloor x \rceil
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <iostream>
 8 #include <cmath>
 9 
10 int main() {
11     // Example of round()
12     std::cout << "Example of round():" << '\n';
13     std::cout << "round(+2.3) = " << std::round(2.3) << '\n'
14         << "round(+2.5) = " << std::round(2.5) << '\n'
15         << "round(+2.7) = " << std::round(2.7) << '\n' << '\n'
16         << "round(-2.3) = " << std::round(-2.3) << '\n'
17         << "round(-2.5) = " << std::round(-2.5) << '\n'
18         << "round(-2.7) = " << std::round(-2.7) << '\n' << '\n';
19 
20     std::cout << "round(-0.0) = " << std::round(-0.0)  << '\n'
21         << "round(-Inf) = " << std::round(-INFINITY) << '\n';
22 }
```

Figure 211

The round function is also part of the standard library header cmath.

* * *

### Arrows

Arrows are often used in function notation. There are a few other areas where you might see them.

#### Material implication

Arrows like the right arrow with capital r and the right arrow in lowercase are sometimes used in logic for material implication. That is, if A is true, then B is also true.

![](resources/math_38.png)

Figure 212

In C++:

```
 1 // From Paper to Code
 2 // Arrows - material implication
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: A \Rightarrow B
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cassert>
 8 
 9 int main() {
10     bool a=true;
11     bool b=true;
12 
13     if (a == true) {
14         assert(b == true);
15     }
16 }
```

Figure 213

Here we use assert to make sure that both a and b are true (Will complain if not).

The arrows can go in either direction: left arrow, right arrow, or both as a left-right arrow. When A is right arrow B, and B is right arrow A, they are said to be equivalent.

![](resources/math_39.png)

Figure 214

#### Equality

In math, the less the, greater than, less than or equal, and greater than or equal are typically used the same way we use them in code. Less than, greater than, less than or equal to, and greater than or equal to, respectively.

In C++:

```
 1 // From Paper to Code
 2 // Arrows - equality
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: https://www.geeksforgeeks.org/inequalities-in-latex/
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     if (50 > 2) {std::cout << "50 is greater then 2." << std::endl;}
10     if (2 < 10) {std::cout << "2 is less then 10." << std::endl;}
11     if (3 <= 4) {std::cout << "3 is less then or equal to 4." << std::endl;}
12     if (4 >= 4) {std::cout << "4 is greater then or equal to 4." << std::endl;}
13 
14 // 50 is greater than 2.
15 // 2 is less than 10.
16 // 3 is less than or equal to 4.
17 // 4 is greater than or equal to 4.
```

Figure 215

You might see a slash through these symbols on rare occasions to describe not. As in, `k` is not greater than `j.`

![](resources/math_40.png)

Figure 216

The left double arrow and right double arrow are sometimes used to represent significant inequality. `k` is an order of magnitude larger than `j.` In mathematics, order of magnitude is rather specific; it is not just a `really big difference.`

![](resources/math_41.png)

Figure 217

In C++:

```
 1 // From Paper to Code
 2 // Arrows - order of magnitude
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k \gg j
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cmath>
 8 
 9 double orderOfMagnitude(double n)
10 {
11     return trunc(log10(n));
12 }
13 
14 int main() {
15     double k=1000.0;
16     double j=0.001;
17 
18     if (orderOfMagnitude(k) > orderOfMagnitude(j))
19     {
20         std::cout << "k is in order of magnitude larger than j." << std::endl;
21     }
22 }
```

Figure 218

Here we check the order of magnitude by taking the `log 10` of `n` and then using trun on the result. Both `log 10` and trunc functions are part of the standard library header cmath.

Running the code, we get that `k` equals `3` and `j` equals `minus 3.` So, `k` is larger in order of magnitude than `j.`

#### Conjunction and Disjunction

Another use of arrows in logic is conjunction and disjunction. They are analogous to a programmer’s `AND` and `OR` operators, respectively.

![](resources/math_42.png) AND OR

An example of a conjunction.

![](resources/math_43.png)

Figure 219

In C++:

```
 1 // From Paper to Code
 2 // Arrows - conjunction & disjunction
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k > 2 \land k <  4 \Leftrightarrow k = 3
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cassert>
 8 
 9 int main() {
10     int k=3;
11 
12     if (k > 2 && k < 4)
13     {
14         assert(k == 3);
15     }
16 }
```

Figure 220

We use assert to verify that `k` is larger than `2` and that `k` is lesser than `4.` The assert explicitly asserts that `k` equals `3.`

As you can see, both sides are equivalent.

In C++:

```
 1 // From Paper to Code
 2 // Arrows - conjunction & disjunction
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: k > 2 \land k <  4 \Leftrightarrow k = 3
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cassert>
 8 
 9 int main() {
10     int k=3;
11 
12     if (k == 3)
13     {
14         assert(k > 2 && k < 4);
15     }
16 }
```

Figure 221

It validates the other way around.

The down arrow is a logical disjunction, like the `OR` operator.

![](resources/math_44.png)

Figure 222

OR

In C++:

```
 1 // From Paper to Code
 2 // Arrows - conjunction & disjunction
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: A \lor B
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 
 8 int main() {
 9     int k=5;
10 
11     if (k == 3 || k == 5)
12     {
13         std::cout << "k is equal to 3 OR 5." << std::endl;
14     }
15 }
```

Figure 223

Here we see that `k` equals `3` or `5.`

* * *

### Logical Negation

Occasionally, the l not, tilde, and exclamation mark symbols represent logical NOT. For example, l not A is only true if A is false. Here is a simple example using the l not symbol:

![](resources/math_45.png)

Figure 224

In C++:

```
 1 // From Paper to Code
 2 // Logical Negation
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: x \neq y \Leftrightarrow \lnot(x = y)
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cassert>
 8 
 9 int main() {
10     int x=5,y=7;
11 
12     if (x != y)
13     {
14         assert(!(x == y));
15     }
16 }
```

Figure 225

We use assert to confirm that `x` is not equal to `y` is the same as `x` equal to `y` negated.

As a side note: The tilde has many different meanings depending on context—for example, row equivalence in matrix theory or the same order of magnitude inequality.

* * *

### Intervals

Sometimes, a function deals with real numbers restricted to some range of values; such a constraint can be represented using an interval.

For example, we can represent the numbers between zero and one, including/not including zero and/or one, as follows.

A rounded left and right bracket is the same as Not including zero or one.

![](resources/math_46.png)

Figure 226

A square left and a round right bracket are the same as including zero but not one.

![](resources/math_47.png)

Figure 227

A round left bracket and a right square bracket are the same, Not including zero but including one.

![](resources/math_48.png)

Figure 228

A square left bracket and a right square bracket are the same, including both zero and one.

![](resources/math_49.png)

Figure 229

For example, we indicate that a point x is in the unit cube in 3D; we do like this in notation.

![](resources/math_50.png)

Figure 230

In C++:

```
 1 // From Paper to Code
 2 // intervals
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: x \in [0, 1]^3
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <cmath>
 8 #include <limits>
 9 #include <vector>
10 
11 int main() {
12     std::vector<double> a = {nextafter(0.0, std::numeric_limits<double>::infinity())\
13 , nextafter(1.0, -std::numeric_limits<double>::infinity())}; // open interval
14     std::vector<double> b = {nextafter(0.0, std::numeric_limits<double>::infinity())\
15 , 1}; // interval closed on the left 
16     std::vector<double> c = {0, nextafter(1.0, -std::numeric_limits<double>::infinit\
17 y())}; // interval closed on the right
18     std::vector<double> d = {0, 1}; // closed interval
19 }
```

Figure 231

The `nextafter` function returns the next representable value of from in the direction of to. The numeric limits class template provides a standardized way to query various properties of arithmetic types.

Intervals are used in conjunction with set operations.

![](resources/math_51.png)

Figure 232

#### Intersection

```
 1 // From Paper to Code
 2 // Intervals - intersection
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: [3, 5) \cap [4, 6] = [4, 5)
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <iostream>
 7 #include <vector>
 8 #include <algorithm>
 9 #include <iterator>
10 int main()
11 {
12     std::vector<int> v1{1,2,3,4,5,6,7,8};
13     std::vector<int> v2{5,7,9,10};
14     std::sort(v1.begin(), v1.end());
15     std::sort(v2.begin(), v2.end());
16 
17     std::vector<int> v_intersection;
18 
19     std::set_intersection(v1.begin(), v1.end(),
20                           v2.begin(), v2.end(),
21         std::back_inserter(v_intersection));
22     for(int n : v_intersection)
23         std::cout << n << ' ';
24 }
```

Figure 233

Here, we use the set intersection function for vector `v1` and vector `v2.` The result is `5 7`

#### Union

```
 1 // From Paper to Code
 2 // Intervals - union
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: [3, 5) \cup [4, 6] = [3, 6]
 5 // Test LaTeX: https://quicklatex.com/
 6 #include <vector>
 7 #include <iostream>
 8 #include <algorithm>
 9 #include <iterator>
10  
11 int main()
12 {
13     {
14         std::vector<int> v1 = {1, 2, 3, 4, 5}; 
15         std::vector<int> v2 = {      3, 4, 5, 6, 7}; 
16         std::vector<int> dest1;
17 
18         std::set_union(v1.begin(), v1.end(),
19                        v2.begin(), v2.end(),                  
20                         std::back_inserter(dest1));
21  
22         for (const auto &i : dest1) {
23             std::cout << i << ' ';
24         }   
25         std::cout << '\n';
26     }
27     {
28         std::vector<int> v1 = {1, 2, 3, 4, 5, 5, 5}; 
29         std::vector<int> v2 = {      3, 4, 5, 6, 7}; 
30         std::vector<int> dest1;
31  
32         std::set_union(v1.begin(), v1.end(),
33                        v2.begin(), v2.end(),                  
34                         std::back_inserter(dest1));
35  
36         for (const auto &i : dest1) {
37             std::cout << i << ' ';
38         }   
39         std::cout << '\n';
40     }
41 }
42 // 1 2 3 4 5 6 7 
43 // 1 2 3 4 5 5 5 6 7
```

Figure 234

Here, we use the set union function for vectors `v1` and `v2`

#### Difference

```
 1 // From Paper to Code
 2 // Intervals - difference
 3 // Run with: https://www.jdoodle.com/online-compiler-c++17/
 4 // LaTeX: [3, 5) - [4, 6] = [3, 4)
 5 // LaTeX: [4, 6] - [3, 5)  = [5, 6]
 6 // Test LaTeX: https://quicklatex.com/
 7 #include <algorithm>
 8 #include <iostream>
 9 #include <iterator>
10 #include <string_view>
11 #include <vector>
12 
13 auto print = [](const auto& v, std::string_view end = "") {
14     std::cout << "{ ";
15     for (auto i : v) std::cout << i << ' ';
16         std::cout << "} " << end;
17 };
18 
19 struct Order // a struct with some interesting data
20 {
21     int order_id;
22 
23     friend std::ostream& operator<<(std::ostream& os, const Order& ord) {
24         return os << ord.order_id << ',';
25     }
26 };
27 
28 int main() {
29     const std::vector<int> v1 {1, 2, 5, 5, 5, 9};
30     const std::vector<int> v2 {2, 5, 7};
31     std::vector<int> diff;
32 
33     std::set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(),
34                         std::inserter(diff, diff.begin()));
35     print(v1, "∖ ");
36     print(v2, "= ");
37     print(diff, "\n");
38 
39     //We want to know which orders "cut" between old and new states:
40     std::vector<Order> old_orders { {1}, {2}, {5}, {9} };
41     std::vector<Order> new_orders { {2}, {5}, {7} };
42     std::vector<Order> cut_orders;
43 
44     std::set_difference(old_orders.begin(), old_orders.end(),
45                         new_orders.begin(), new_orders.end(),
46                         std::back_inserter(cut_orders),
47                         [](auto& a, auto& b) { return a.order_id < b.order_id; });
48 
49     std::cout << "old orders = "; print(old_orders, "\n");
50     std::cout << "new orders = "; print(new_orders, "\n");
51     std::cout << "cut orders = "; print(cut_orders, "\n");
52 }
53 // { 1 2 5 5 5 9 } ∖ { 2 5 7 } = { 1 5 5 9 } 
54 // old orders = { 1, 2, 5, 9, } 
55 // new orders = { 2, 5, 7, } 
56 // cut orders = { 1, 9, }
```

Figure 235

* * *

## Extra

### Challenge 1 - PixMap to SVG in Modern C++

The journey of mastering 2D computer graphics in Modern C++ culminates in a stimulating challenge: developing your own tracer to convert PPM files into SVG format. This endeavor not only tests your proficiency but also enhances your understanding of vector graphics and image processing. In this task, you are encouraged to draw inspiration from an existing tool, vtracer, a robust raster-to-vector graphics converter. Detailed information about vtracer can be found at [vtracer on GitHub](https://github.com/visioncortex/vtracer).

To begin, it’s crucial to understand the mechanics behind vtracer. This tool exemplifies the art of transforming pixel-based images into scalable vector graphics. Its underlying algorithm is a testament to the harmonious blend of image processing and vectorization techniques. The algorithm’s comprehensive details, which will serve as a guiding framework for your implementation, are thoroughly explained at [vtracer documentation](https://www.visioncortex.org/vtracer-docs).

Your implementation should be rooted in modern C++ practices, showcasing not only technical competence but also the elegance and efficiency of modern coding standards. Embrace C++’s powerful features to create a solution that’s both effective and efficient, reflecting the advancements in the language since the inception of traditional image processing tools.

One of the key components of your implementation will be handling PPM files. For this, you should utilize the `ppmpp.hpp` library, an efficient and modern C++ library for PPM file manipulation. It provides a streamlined and intuitive interface for handling PixMap files, essential for your tracer’s input processing. You can find more about `ppmpp.hpp` at [ppmpp on GitHub](https://github.com/chbtoys/ppmpp).

In crafting your tracer, focus on the conversion accuracy and the optimization of the output SVG files. The challenge lies not only in accurately tracing the outlines and features of the input image but also in optimizing the vector graphics for minimal file size without compromising the visual fidelity. This balance is crucial in creating scalable and efficient SVG files.

As you embark on this journey, remember that error handling and code robustness are as important as the core functionality. Your tracer should be equipped to handle various edge cases and input anomalies, ensuring a smooth and reliable conversion process. This will not only demonstrate your technical prowess but also your foresight in creating user-centric applications.

This project is more than a mere exercise in coding. It’s an opportunity to delve deep into the realms of computer graphics, image processing, and modern C++ programming. By completing this challenge, you will not only have created a valuable tool but also have taken a significant leap in your understanding of these interconnected domains. This endeavor, standing at the intersection of creativity and technicality, is sure to be a rewarding climax to your exploration of 2D Computer Graphics in Modern C++.

* * *

### Challenge 2 - PixMap Converted To Rotated Filled Blended Ellipses in Modern C++

In the realm of 2D Computer Graphics with Modern C++, an intriguing and complex challenge awaits: creating a software that converts PPM files into SVG format using rotated, filled, blended ellipses. This task is not only a test of programming skill but also an exploration into the blend of art and algorithm. The inspiration for this challenge comes from the tool known as Primitive, which is detailed at [Primitive on GitHub](https://github.com/fogleman/primitive). This tool masterfully recreates images using simple geometric shapes, providing a foundation upon which to build your project.

Your task is to create a modern C++ application that employs hill climbing and simulated annealing algorithms to iteratively improve the quality of the generated SVG image. These optimization algorithms, commonly used in artificial intelligence and mathematical optimization, can be explored in more detail at [Hill Climbing on Wikipedia](https://en.wikipedia.org/wiki/Hill_climbing) and [Simulated Annealing on Wikipedia](https://en.wikipedia.org/wiki/Simulated_annealing). The challenge is to adapt these algorithms for image processing, making artistic decisions about shape placement, rotation, and color blending.

The core of your project will involve interpreting PPM files, a popular image format in the graphics community. Handling these files effectively is crucial, and for this, you should integrate the `ppmpp.hpp` library, a modern C++ library tailored for PPM file manipulation. Its capabilities and usage are further explained at [ppmpp on GitHub](https://github.com/chbtoys/ppmpp). This library will serve as the backbone for your image processing and conversion task.

Your implementation should focus on creating SVG images composed entirely of ellipses. These ellipses, varying in size, orientation, color, and blending levels, must be strategically placed to replicate the original PPM image as closely as possible. This requires a deep understanding of color theory, geometry, and algorithmic optimization to achieve a harmonious and aesthetically pleasing result.

The challenge lies not only in accurately reproducing the input image but also in doing so with a minimal number of ellipses. This constraint will push you to optimize your algorithm for both performance and output quality. You must strike a balance between the fidelity of the recreated image and the efficiency of the computational process.

To achieve this, you will need to delve into the nuances of modern C++ programming. Your solution should showcase the power and elegance of C++, leveraging features like smart pointers, lambda expressions, and the Standard Template Library (STL) to build a robust and efficient application. Your code should be a testament to the capabilities of C++ in handling complex algorithmic challenges and graphical computations.

This project is not only a technical endeavor but also an artistic one. It requires a keen eye for detail and an appreciation for visual aesthetics. Your program should not just replicate images mechanically but should also capture the essence and mood of the original, using ellipses as a creative medium.

Completing this challenge will mark a significant milestone in your journey through the world of modern C++ and 2D computer graphics. It is a testament to your skills in algorithmic programming, image processing, and artistic expression. This project is more than just an exercise in coding; it is a bridge between the technical and the creative, a fusion of logic and art.

* * *

### Challenge 3 - PixMap Converted to an Oil Painting Using Genetic Drawing in Modern C++

In the dynamic world of 2D Computer Graphics with Modern C++, a new and fascinating challenge emerges: creating a genetic drawing software that transforms a PPM file into an oil painting-like image. This challenge not only encapsulates the essence of computer graphics but also bridges the gap between algorithmic complexity and artistic expression. The concept is inspired by the innovative approach of Genetic Drawing, as explored in [Genetic Drawing on GitHub](https://github.com/anopara/genetic-drawing).

Your objective is to design and implement a software in modern C++ that employs a genetic algorithm to iteratively evolve a random set of brush strokes into a coherent image that resembles an oil painting. This process mimics natural selection, where each iteration or ‘generation’ of the image is evaluated for its closeness to the target image, guiding the algorithm towards a better representation. To understand the underlying principles of this technique, explore resources like this [YouTube playlist on Genetic Algorithms](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6bJM3VgzjNV5YxVxUwzALHV) and Shahriyar Shahrabi’s article on [Procedural Paintings with Genetic Evolution Algorithm](https://shahriyarshahrabi.medium.com/procedural-paintings-with-genetic-evolution-algorithm-6838a6e64703).

The heart of your project is the processing of PPM files, a format well-recognized in graphics programming. For handling these files efficiently, the `ppmpp.hpp` library, a modern C++ library dedicated to PPM file manipulation, should be integrated into your solution. It provides a robust platform for handling image data, which is crucial for your application. More details on `ppmpp.hpp` can be found at [ppmpp on GitHub](https://github.com/chbtoys/ppmpp).

Your implementation should adeptly handle the nuances of genetic algorithms, such as selection, crossover, and mutation, to evolve brush strokes that collectively represent the original image. The challenge is to simulate the texture and color blending typical of oil paintings, using algorithmically generated brush strokes. This requires a deep understanding of genetic algorithms, along with a keen sense of artistic styling in digital media.

The efficiency of the algorithm is paramount. Your solution should not only strive for visual accuracy but also for computational efficiency. This involves optimizing the genetic algorithm to converge towards a satisfactory image in as few generations as possible, thus balancing the computational load with the quality of the output.

Modern C++ offers a plethora of features that are perfect for this task. Smart pointers, advanced data structures, and concurrency features should be harnessed to manage the complex data and processing requirements of this application. Your code should be a showcase of modern C++ best practices, emphasizing clean, efficient, and maintainable code.

In addition to the technical implementation, this challenge also involves an artistic aspect. The goal is not to create a pixel-perfect copy of the original image but rather to reinterpret it as an oil painting, imbued with the unique characteristics that this medium offers. This requires an artistic eye, to ensure that the algorithm captures the essence and mood of the original image, while presenting it in a new, artistic light.

This project represents a perfect culmination of the skills and knowledge you have acquired throughout your journey in 2D Computer Graphics with Modern C++. It challenges you to blend the precision of algorithms with the fluidity of art, leading to the creation of something truly unique and beautiful. This endeavor is not just a test of your programming skills, but also an exploration of the intersection between technology and art, showcasing the vast potential of computer graphics.

* * *

## Final Words

First and foremost, I would like to extend my heartfelt gratitude to you for investing your time and energy in completing ‘2D Computer Graphics in Modern C++ and Standard Library’. Your dedication to exploring and mastering the concepts presented in this book is commendable and indicative of your passion and commitment to computer graphics. It is readers like you, eager to learn and apply new knowledge, who inspire authors like myself to delve into these subjects and present them in a comprehensive and accessible manner.

I hope the journey through this book’s pages has been both enlightening and enjoyable for you. Writing this book was also a journey of discovery for me, driven by a desire to share the fascinating world of 2D computer graphics using the powerful capabilities of modern C++ and the Standard Library. Your willingness to engage with this material, grapple with its complexities, and apply its lessons is deeply appreciated. I hope the knowledge you have gained will serve as a solid foundation for future projects and endeavors in computer graphics or any other area where these skills may be applied.

Lastly, I encourage you to continue exploring and expanding your computer graphics and programming skills. The field constantly evolves, and there is always more to learn and discover. Your feedback, insights, and experiences as a reader are invaluable, and I would be delighted to hear about how you have applied the concepts from the book in your work. Thank you once again for your time and commitment. Enthusiastic and curious readers like you make the effort to write such a book worthwhile.

* * *

![](resources/mathend.jpg)

Figure 236