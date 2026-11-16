![](bbox=[0.18, 0.11, 0.55, 0.23])

Figure 10.10 The eight directions (for 8-neighbor) and four directions (for 4-neighbor) in which one might step going from one pixel to another around a boundary.

attractiveness, strategies based on moments do have problems, not the least of which is sensitivity to quantization and sampling [10.24]. (See Assignments for this chapter.)

The use of moments is actually a special case of a much more general approach to image matching [10.30] referred to as the method of normalization. In this approach, we first transform the region into a canonical frame by performing a (typically linear) transform on all the points. The simplest such transformation is to subtract the coordinates of the center of gravity (CG) from all the pixels, thus moving the coordinate origin to the CG of the region. In the more general case, such a transformation might be a general affine transform, including translation, rotation, and shear. We then do matching in the transform domain, where all objects of the same class (e.g., triangles) look the same.

Some refinements are also required if moments are to be calculated with grayscale images, that is, when the f of Eq. 10.50 is not simply a one or a zero. All the theory of invariance still holds, but as Gruber and Hsu [10.13] point out, noise corrupts moment features in a data-dependent way.

Once a program has extracted a set of features, this set can be used either to match two observations or to match an observation to a model. The use of simple features in matching is described in section 10.5.1.

# 10.4.3 Chain Codes

A chain code is a feature describing the boundary of a region. In a chain code, a walk around a region is represented by a sequence of numbers, all between 0 and 7 (if using eight directions) or between 0 and 3 (if using four directions), designating the direction of each step. The eight and four cardinal directions are defined as illustrated in Figure 10.10. The boundary of a region may then be represented by a string of single digits. A more compact representation utilizes superscripts whenever a direction is repeated. For example, 001212776660 could be written 0^2 12^1 27^2 6^4 0, and illustrates the boundary shown in Figure 10.11. The ability to describe boundaries with a sequence of symbols plays a significant role in the discipline known as syntactic pattern recognition, and appears in the Computer Vision literature. Such a representation allows recognition of shapes using principles from compiler theory.

# 10.4.4 Fourier Descriptors

In this section, we discuss a frequency-domain representation for shape. The title “Fourier Descriptor” is used for historical reasons. However, by the definition of this book,