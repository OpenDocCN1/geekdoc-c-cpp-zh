Utilization: Data-processing and visualization tasks are typically written as shell scripts that construct and execute a datalow pipeline by cascading the Teem basic filters. This is the easiest and most rapid way to use Teem to produce visualizations. If desired, Teem can be also used in terms of libraries providing APIs. Teem is not end-user software. As such, it does not provide user interface or interaction functions present in complete visualization applications. However, its generic, modular, and coherent API design allow such applications to be built on top of it. For example, the SCIRun and 3D Slicer applications integrated the functionality of Teem to provide high-level imaging capabilities.

# ImageJ

Type: Turnkey
Availability: Open source (written in Java)
Address: http://rsbweb.nih.gov/ij/
Description: ImageJ is an application conceived for the easy processing of 2D images. Inspired by classical 2D image manipulation programs, ImageJ offers a wide set of basic image processing operations, such as contrast enhancement, smoothing, sharpening, denoising, edge detection; advanced image processing such as segmentation and manipulating stacks of 2D images, image sequences, or separate channels of the same image; and computing various image statistics and measurements, such as histograms and image calibration. Written in Java, ImageJ is optimized for the efficient processing of large images, using multithreading.
Utilization: In typical end-user mode, ImageJ offers its processing capabilities via GUIs and a range of direct selection and manipulation tools. Basic functionality is extendable via a relatively easy-to-use plug-in in Java interface. As such, hundreds of third-party plug-ins has been developed for ImageJ for both general-purpose image processing but also for specialized manipulation of various types of microscopy, biology, and medical images. Basic operations can be composed in so-called macros by using a built-in scripting language. Given the rich set of available plug-ins, ImageJ is a very competitive alternative to MATLAB for 2D image processing.

# Binvox

Type: Turnkey utility
Availability: Open source (written in C/C++)
Address: http://www.cs.princeton.edu/~min/binvox