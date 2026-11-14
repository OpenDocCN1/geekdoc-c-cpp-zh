+   * Grayness ambiguity
+   * Geometrical fuzziness
+   * Vague (complex/ill-defined) knowledge

These problems are fuzzy in nature. The question of whether a pixel should become darker or brighter than it already is, the question regarding the boundary between two image segments, and the question of what is a tree in a scene analysis problem, all of these and other similar questions are examples of situations that can be best managed by a fuzzy approach.

As an example, we can regard the variable “color” as a fuzzy set. It can be described with the membership set:

```
color = [red, yellow, green, blue]
```

The noncrisp boundaries between the colors can be represented in a much better manner. This is shown in Figure 15.3.

# 15.2.2 Fuzzy Classifier

Image classification and segmentation were presented in Chapter 12, and it was observed there that the simple nearest neighbor rule can be easily implemented to segment similar pixels together. However, it required a teacher (supervised learning) to identify parts of the classes to be segmented. Fuzzy c-means clustering is a technique that can be used for classifying data based on their dynamics of clustering around certain deduced centers. This does not necessarily need a training set, and can be used to perform the classification on images. The different theoretical components of fuzzy image processing provide diverse possibilities for development

![](bbox=[0.21, 0.75, 0.82, 0.9])

FIGURE 15.3 Fuzzy membership representing color space.