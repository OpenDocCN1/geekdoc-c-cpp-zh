# # Chapter 13

# # Camera Specifications
and Transformations

# ## 13.1 Introduction

In this chapter, we briefly discuss camera specifications, which you already encountered in Chapter 6. Recall that we specified a camera in WPF in code like that shown below:

```
~~~xml
<PerspectiveCamera
    Position="57, 247, 41"
    LookDirection="-0.2, 0, -0.9"
    UpDirection="0, 1, 0"
    NearPlaneDistance="0.02" FarPlaneDistance="1000"
    FieldOfView="45"
    />
~~~
```

From such a specification, we will create a sequence of transformations that will transform the world coordinates of a point on some model to so-called “camera coordinates,” and from there to image coordinates. We'll do so by repeatedly using the Transformation Uniqueness principle.

Since an affine coordinate frame in three dimensions consists of four noncoplanar points, that says that if we know where we want to send each of four noncoplanar points, we know that there's exactly one affine transformation that will do it for us. The corresponding theorem for the plane says that if we know where we want to send some three noncollinear points, then there's a unique affine transformation that will do it.

We start with an example of this kind of transformation in the plane. Next we discuss basic perspective camera specifications and how we can convert such specifications to a set of affine transformations, plus one projective transformation. We briefly treat the case of “parallel” cameras, and discuss the details of that case and of skewed projections, in this chapter’s web materials.