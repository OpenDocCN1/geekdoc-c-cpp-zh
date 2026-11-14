# 19.8.1 Lane Departure Detection Implementation and Acceleration

The project was designed and developed by Aaron Severance of the University of Washington, Seattle, WA, November 2005.

# 19.8.1.1 Introduction

A recent advance in safety technology in the automotive industry has been the design of lane departure detection systems. These systems are designed to alert an unaware driver that his or her vehicle has started to leave the designated lane. Such a system can be very useful in alerting tired or distracted drivers of their potentially harmful state.

In order to function properly, such a system must be able to handle different size, color, shape, and spacing of lane markings. One popular approach is to use a forward-looking camera, mounted in the windshield of the vehicle, to examine the road. This approach's utility lies in its ability to analyze a large field of information and to be easily adapted/upgraded, something that approaches utilizing specialized sensors lack.

Algorithmically, this can be accomplished using three main steps: edge detection, line finding, and image space conversion. Edge detection is the process of reducing the amount of information to be analyzed by selecting only portions of the image with a strong gradient. Line finding does a transformation on the image in order to detect predominant lines in the image, which should correspond to lane markings. Finally, image space conversion converts the positions of the lines found in the image to positions in a real-world coordinate system, relative to the position of the vehicle.

Implementation was done as a dual core processor system on a Xilinx Spartan-III FPGA. The hardware and software configurations were created using Xilinx Platform Studio 6.2i, which included the MicroBlaze soft processor core that was used in the design. In addition, Xilinx State CAD was used in order to design the custom hardware acceleration logic.

# 19.8.1.2 Requirements

The lane detection problem reduces to two tasks: edge detection followed by line finding.

# 19.8.1.2.1 EDGE DETECTION

To identify an edge within a visual field, a region of the input must be specified to be the region of interest (ROI). The edge detection routine must have an output that corresponds to convolving the image with a 3x 3 Sobel vertical edge detection filter in the ROI. Any pixels in the image not in the ROI must be set to zero. The convolution must not be circular; the outermost pixels of the image, where a full convolution cannot be performed, must be set to zero. Finally, a threshold input must be specified; pixels with edge strength below this threshold must be set to zero.

# 19.8.1.2.2 LINE FINDING

Line finding was implemented using the Hough Transform, with the output bin of angles equal in number to the input width of the image. Each of the left/right halves of the image must be searched for one lane marking, with at least r/2 angles scanned. A line finding algorithm must be able to identify the two peaks with the highest value in the output of the Hough Transform as probable lane markings. An inverse Hough Transform must be provided; this will allow for output to an image buffer of the lines identified as lane markings.