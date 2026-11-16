# 11.2 Matching Iconic Representations

# 11.2.1 Matching Templates to Scenes

Recall that an iconic representation of an image is an image, e.g., a smaller image, an image that is not blurred, etc. In this section, we need to match two images.

A template is a representation for an image (or sub-image) that is itself an image, but almost always smaller than the original. A template is typically moved around the target image until a location is found that maximizes some match function. The most obvious such function is the sum squared error, sometimes referred to as the sum-squared difference (SSD),

\( SSD(x, y) = \left( \sum_{u=1}^N \sum_{v=1}^N (f(x+u, y+v) - T(u, v)) \right)^2 \, , \) (11.1)

which provides a measure of how well the template (T) matches the image (f) at point x, y, assuming the template is N x N. If we expand the square and carry the summation through, we find1

\( SSD(x, y) = \sum_{u, v} f^2(x+u, y+v) - 2 \sum_{u, v} f(x+u, y+v) T(u, v) + \sum_{u, v} T^2(u, v). \) (11.2)

In this equation, the template indices are denoted as ranging from 1 to N. However, the origin of the template could be arbitrarily defined to be in the center of the template, and in that case, the template indices could have negative values without any loss of generality.

Let's look at these terms: The first term is the sum of the squared image brightness values at the point of application. It says nothing about how well the image matches the template (although it IS dependent on the image). The third term is simply the sum of the squared elements of the template, and is a constant, no matter where the template is applied. The second term, containing both the image and the template, is the key to matching, and that term is the correlation.

We have seen correlation many times in this book. For example, an edge detector actually looks like an edge, a fact that a kernel operator detects using correlation. Correlation occurs over and over again. Due to the image dependency in the first term of Eq. 11.2, the use of maximum of correlation for matching isn't quite the same as minimizing the SSD, and that difference can cause problems and require normalization.

# Normalized Correlation

To make correlations less sensitive to variations in lighting they may be normalized by modifying both the image and the template by:

+   - Computing the mean of the image in the region under the template, denoted \(\hat{f}(x, y)\).
+   - Computing the mean of all the points in the template, denoted \(\hat{T}\).