
![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_75_0.png)

**Figure 3.15**  
Perspective view volume or frustum.

The perspective matrix is used to transform points in 3D space to their appropriate position on the near clipping plane, and is built by first computing values q, A, B, and C, and then using those values to construct the matrix, as shown in Figure 3.16 (and derived in [WB15]).

$$
q = \frac{1}{\tan\left(\frac{\text{FieldOfView}}{2}\right)}
$$

$$
A = \frac{q}{\text{aspectRatio}}
$$

$$
B = \frac{Z_{\text{near}} + Z_{\text{far}}}{Z_{\text{near}} - Z_{\text{far}}}
$$

$$
C = \frac{2 \cdot (Z_{\text{near}} \cdot Z_{\text{far}})}{Z_{\text{near}} - Z_{\text{far}}}
$$

$$
\begin{bmatrix}
A & 0 & 0 & 0 \\
0 & q & 0 & 0 \\
0 & 0 & B & C \\
0 & 0 & -1 & 0
\end{bmatrix}
$$

**Figure 3.16**  
Building a perspective matrix.

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_78_0.png)

We could encode this as a simple Java/JOGL utility function that builds a look-at matrix, given specified values for camera location, target location, and the initial “up” vector Ŷ. Since JOML includes the function Mat4f.setLookAt() for building a look-at matrix, we will simply use that. This function will be useful later in this textbook, particularly in Chapter 8 when we generate shadows.

### 3.10 GLSL FUNCTIONS FOR BUILDING MATRIX TRANSFORMS

Although JOML includes predefined functions for performing many of the 3D transformations covered in this chapter, such as translation, rotation, and scale, GLSL only includes basic matrix operations such as addition, concatenation, and so on. It is therefore sometimes necessary to write our own GLSL utility functions for building 3D transformation matrices when we need them to perform certain 3D computations in a shader. The appropriate datatype to hold such a matrix in GLSL is mat4.

The syntax for initializing mat4 matrices in GLSL loads values by columns. The first four values are put into the first column, the next four into the next column, and so forth, as illustrated in the following example:

```glsl
mat4 translationMatrix =
    mat4( 1.0, 0.0, 0.0, 0.0,    // note this is the leftmost column, not the top row
           0.0, 1.0, 0.0, 0.0,
           0.0, 0.0, 1.0, 0.0,
           tx, ty, tz, 1.0 );
```

which builds the translation matrix described previously in Figure 3.3.

Program 3.1 includes five GLSL functions for building 4x4 translation, rotation, and scale matrices, each corresponding to formulas given earlier in this chapter. We will use some of these functions later in the book.

### Program 3.1 Building Transformation Matrices in GLSL

```glsl
// builds and returns a translation matrix
mat4 buildTranslate(float x, float y, float z)
{
    mat4 trans = mat4(1.0, 0.0, 0.0, 0.0,
                      0.0, 1.0, 0.0, 0.0,
                      0.0, 0.0, 1.0, 0.0,
                      x, y, z, 1.0 );
    return trans;
}

// builds and returns a matrix that performs a rotation around the X axis
mat4 buildRotateX(float rad)
{
    mat4 xrot = mat4(1.0, 0.0, 0.0, 0.0,
                     0.0, cos(rad), -sin(rad), 0.0,
                     0.0, sin(rad), cos(rad), 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return xrot;
}

// builds and returns a matrix that performs a rotation around the Y axis
mat4 buildRotateY(float rad)
{
    mat4 yrot = mat4(cos(rad), 0.0, sin(rad), 0.0,
                     0.0, 1.0, 0.0, 0.0,
                     -sin(rad), 0.0, cos(rad), 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return yrot;
}

// builds and returns a matrix that performs a rotation around the Z axis
mat4 buildRotateZ(float rad)
{
    mat4 zrot = mat4(cos(rad), -sin(rad), 0.0, 0.0,
                     sin(rad), cos(rad), 0.0, 0.0,
                     0.0, 0.0, 1.0, 0.0,
                     0.0, 0.0, 0.0, 1.0 );
    return zrot;
}

// builds and returns a scale matrix
mat4 buildScale(float x, float y, float z)
{ mat4 scale = mat4(x, 0.0, 0.0, 0.0,
                    0.0, y, 0.0, 0.0,
                    0.0, 0.0, z, 0.0,
                    0.0, 0.0, 0.0, 1.0 );
  return scale;
}
```

## SUPPLEMENTAL NOTES

In this chapter we have seen examples of applying matrix transformations to points. Later, we will also want to apply these same transforms to vectors. In order to accomplish a transform on a vector V equivalent to applying some matrix transform M to a point, it is necessary in the general case to compute the *inverse transpose* of M, denoted (M⁻¹)ᵀ, and multiply V by that matrix. In some cases, M=(M⁻¹)ᵀ, and in those cases it is possible to simply use M. For example, the basic rotation matrices we have seen in this chapter are equal to their own inverse transpose and (therefore also) to points. Thus, the examples in this book sometimes use (M⁻¹)ᵀ when applying a transform to a vector, and sometimes simply use M.

Many of the JOML functions described in this section modify a specified matrix and (somewhat counterintuitively) return a reference to the same matrix, rather than building and returning a new matrix. This is for performance reasons, and will be discussed in greater detail in Chapter 4.

One of the things we haven’t discussed in this chapter is techniques for moving the camera smoothly through space. This is very useful, especially for games and CGI movies, but also for visualization, virtual reality, and 3D modeling. Code that does this is called a *camera controller*, and there are many resources available online for this topic [TR15].

We didn’t include complete derivations for all of the matrix transforms that were presented (they can be found in other sources, such as [FV95]). We strove instead for a concise summary of the point, vector, and matrix operations necessary for doing basic 3D graphics programming. As this book proceeds, we will encounter many practical uses for the methods presented.

## Exercises

- 3.1 Modify Program 2.5 so that the vertex shader includes one of the buildRotate() functions from Program 3.1 and applies it to the points comprising the triangle. This should cause the triangle to be rotated from its original orientation. You don't need to animate the rotation.

- 3.2 *(RESEARCH)* At the end of Section 3.4 we indicated that Euler angles can in some cases lead to undesirable artifacts. The most common is called "gimbal lock." Describe gimbal lock, give an example, and explain why gimbal lock can cause problems.

- 3.3 *(RESEARCH)* One way of avoiding the artifacts that can manifest when using Euler angles is to use *quaternions*. We didn't study quaternions; however, JOML includes a Quaternionf class. Do some independent study on quaternions, and familiarize yourself with the related JOML Quaternionf class.

## References

- [CR86] C. Crivelli, *The Annunciation, with Saint Emidius* (1486), in the National Gallery, London, England, accessed July 2020, https://www.nationalgallery.org.uk/paintings/carlo-crivelli-the-annunciation-with-saint-emidius

- [EU76] L. Euler, *Formulae generales pro translatione quacunque corporum rigidorum* (General formulas for the translation of arbitrary rigid bodies), Novi Commentarii academiae scientiarum Petropolitanae 20, 1776.

- [FV95] J. Foley, A. van Dam, S. Feiner, and J. Hughes, *Computer Graphics—Principles and Practice*, 2nd ed. (Addison-Wesley, 1995).

- [KU98] J. B. Kuipers, *Quaternions and Rotation Sequences* (Princeton University Press, 1998).

- [TR15] T. Reed, OpenGL Part 3B: Camera Control (blog). Accessed March 2021, https://www.trentreed.net/blog/qt5-opengl-part-3b-camera-control

- [WB15] W. Brown, LearnWebGL (2015), chapter 8.2 (Orthographic Projections), Accessed March 2021, http://learnwebgl.brown37.net/08_projections/projections_ortho.html

A related structure in OpenGL is called a *Vertex Array Object*, or *VAO*. VAOs were introduced in version 3.0 of OpenGL and are provided as a way of organizing buffers and making them easier to manipulate in complex scenes. OpenGL requires at least one VAO to be created, and for our purposes one will be sufficient.

For example, suppose that we wish to display two objects. On the Java/JOGL side, we could do this by declaring a single VAO and an associated set of two VBOs (one per object), as follows:

```java
private int vao[] = new int[1];    // OpenGL requires these values be specified in arrays
private int vbo[] = new int[2];
...
gl.glGenVertexArrays(1, vao, 0);
gl.glBindVertexArray(vao[0]);
gl.glGenBuffers(2, vbo, 0);
```

The two OpenGL commands glGenVertexArrays() and glGenBuffers() create VAOs and VBOs, respectively, and produce integer IDs for these items that are stored in the arrays vao and vbo. The purpose of glBindVertexArray() is to make the specified VAO “active” so that the generated buffers¹ will be associated with that VAO.

A buffer needs to have a corresponding *vertex attribute* variable declared in the vertex shader. Vertex attributes are generally the first variables declared in a

![](img/70923e8fd7afb5b4f7fd45b2d2275dfd_85_0.png)

¹ Throughout this example, two buffers are declared, to emphasize that *usually* we will use several buffers. Later we will use the additional buffer(s) to store other information associated with the vertex, such as color. In the current case we are using only one of the declared buffers, so it would have been sufficient to declare just one VBO.
