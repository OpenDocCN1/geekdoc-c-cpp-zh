In the first case, geometric characteristics of faces to be matched, such as distances between different facial features, are compared. This technique provides limited results, although it has been used extensively in the past. In the second case, face images represented as a two-dimensional array of pixel intensity values are compared to a single or several templates representing the whole face. More successful template-matching approaches use principal components analysis (PCA) or linear discriminant analysis (LDA) to perform dimensionality reduction, achieving good performance at a reasonable computational complexity/time. Other template-matching methods use neural network classification and deformable templates, such as elastic graph matching (EGM).

The appearance of the human face image has potentially very large intra-subject variations due to 3D head pose:

+   * Illumination (including indoor/outdoor)
+   * Facial expression
+   * Face angle or position
+   * Occlusion due to other objects or accessories (e.g., sunglasses, scarf, etc.)
+   * Facial hair
+   * Aging

A number of face recognition algorithms, along with their modifications, have been developed during the past several decades (see Figure 14.1). As can be seen from the figure, each domain has its own techniques and algorithms to perform the task. By no means is this an exhaustive representation of all the existing techniques; newer and better techniques keep emerging. However, this figure gives an overall idea of where the focus should be for a particular group with a specific interest/expertise.

In this chapter, the focus is on the use of PCA with statistical distance measurements to distinguish faces from one another. As can be sensed from these statements, all this requires a lot of matrix manipulation, and this is discussed next.

# 14.3 VECTOR REPRESENTATION OF IMAGES

Image data can be represented as vectors, that is, as points in a high-dimensional vector space. For example, a p × q 2D image can be mapped to a vector x ∈ ℜ^n by lexicographic ordering of the pixel elements (such