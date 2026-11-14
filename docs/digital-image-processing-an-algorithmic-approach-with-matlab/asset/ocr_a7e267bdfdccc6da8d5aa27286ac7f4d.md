display, delay time between adjacent image frames, background color, and transition information.

# 2.2.4 TIFF Format

The TIFF format is controlled by a specification jointly written by Aldus Corporation and Microsoft. The format was designed to incorporate various formats with a futuristic vision. It is a complicated and platform-independent format made up of three unique data structures: Image File Header (IFH), Image File Directory (IFD), and Directory Entry (DE). The format is very similar to BMP, at least in terms of storage and usage.

Any of these formats can also be used for writing an image from MATLAB workspace to the secondary storage. The function imwrite() is used for this purpose and will be further discussed in Section 2.5.

# 2.3 BASICS OF COLOR IMAGES

Similar to several other achievements in the areas of science and engineering that were inspired by nature, image processing takes its inspiration from the best imaging system in nature, the human eye. The photo-sensitive area of the eye is called the retina, which contains two types of light-sensitive cells called rods and cones (according to their shapes). Rods are responsible for producing the sensation of light intensity as well as perception of boundaries and edges in a view scene. The cones are responsible for color perception. These are of three types and are commonly called S-, L-, and M-type cells. The responses of the cone cells were experimentally recorded in the late 1970s, based on the maximum excitation of the cells with respect to a particular frequency of the incident light. Light of variable frequency would represent a particular color for a particular frequency. The responses of the three cone cells were found to be maximum for 420, 534, and 564 nm, respectively. These wavelengths (and consequently, the frequencies) correspond to blue, green, and red colors, respectively. Hence, it was discovered that human color perception is based on a triad of fundamental colors, RGB, which has since remained the most fundamental color model used in digital image processing. Figure 2.4 shows the human eye and the sensory cells along with the sensitivity curves for the RGB model.

This forms the basis of the most fundamental color model system called the RGB (Red, Green, Blue). In fact, once an image is loaded into