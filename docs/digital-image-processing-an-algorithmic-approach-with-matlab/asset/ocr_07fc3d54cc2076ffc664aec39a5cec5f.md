![](bbox=[0.203, 0.068, 0.746, 0.342])

FIGURE 8.2 “Benefit” of a bit is the decrease in distortion due to receiving that bit.

In this approach, we keep reducing one bit at a time until we achieve optimality either in distortion or target rate, or both. An alternate approach is to initially start with zero bits allocated for all classes, and then to find the class that is most “benefited” by getting an additional bit. The benefit for a class is defined as the decrease in distortion for that class. Typically, it is defined by a decreasing parabolic curve, as shown in Figure 8.2.

As shown earlier, the benefit of a bit is a decreasing function of the number of bits allocated previously to the same class. Both approaches mentioned earlier can be used for the bit allocation problem.

Consider the same image as in Figure 8.1(a), this time we do not transform the image as a whole. Rather, the image is divided up into smaller blocks of a predefined size, and the DCT is calculated for each block independently. Each DCT block is then reverse-transformed to obtain the original image. This is shown in Figure 8.3.

# 8.5 QUANTIZATION

Quantization refers to the process of approximating the continuous set of values in the image data with a finite (preferably a much smaller) set of values. The input to a quantizer is the original data, and the output is always one among a finite number of levels. The quantizer is a function whose output values are discrete, and usually finite. Obviously, this is a process