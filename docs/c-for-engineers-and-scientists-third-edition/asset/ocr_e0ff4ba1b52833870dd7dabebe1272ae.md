# Preliminaries

# 1.1 Preliminary One: Unit Analysis

In all fields of study, using consistent and correct units when making computations is crucial. As a simple example, consider the area of a rectangle by this formula:

$Area = length \times width \quad [Eq. 1-1]$

When using this formula, the units for length and width must be the same. Therefore, if the length is given as 2 feet and as 3 inches, at least one of the units must be converted to ensure that both length and width are in the same units before the area is calculated. Converting the length to inches, the rectangle's area is computed as follows:

$Area = 2\ft \times \frac{12\in}{1ft} \times 3\in = 36in^2 \quad [Eq. 1-1a]$

Similarly, if you choose to convert the width from 3 inches to its equivalent feet, the calculation becomes the following:

$Area = 2\ft \times 3 \times \frac{1ft}{12\in} = 0.25ft^2 \quad [Eq. 1-1b]$

In the same manner, if one side of the rectangle is given in centimeters and the other in meters, a conversion is necessary to compute the area. Note that in Equations 1-a and 1-b, units for both length and width as well as the conversion factor ($12\in/1ft$ in Eq. 1-a and $1ft/12\in$ in Eq. 1-b) are included in the final result. The reason is that the terms for units can be multiplied and divided to provide the final unit. Many over this technique is a powerful one for selecting a correct conversion factor and ensuring that a computation is calculated correctly.

To see why, continue with the area example. Use Eq. 1-a, but include only the unit terms, which yields the following:

$Area = ft \times (\frac{m}{ft}) \times in \quad [Eq. 1-1c]$

Now a unit of ft divided by a unit of ft is 1. That is, you can cancel the ft units in Eq. 1-c as follows, which yields the final units as multiplied by in, or $in^2$, which is a correct unit for the area:

$Area = (\frac{in}{ft}) \times in = in^2$

Including only the units and conversion factors in an equation, and canceling out corresponding units in the numerator and denominator, is referred to as performing a unit analysis. As an example of a unit analysis for selecting a correct form of a conversion factor, assume you need to convert miles (symbol mi) to kilometers (symbol km), and you have the information that $1\ Kilometer = 0.6214\ miles$. As a conversion factor, this equality can be written as one of the following fractions:

$\frac{1\km}{mi} = \frac{0.6214\mi}{1}$

Deciding which conversion factor to use in converting miles to kilometers is easier when you consider units. To see why, try both factors with miles, canceling the units that occur