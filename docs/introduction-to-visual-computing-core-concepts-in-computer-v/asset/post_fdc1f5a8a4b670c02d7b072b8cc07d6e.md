
![](img/66c45bbed85bb7ba7f7b05dff49b5060_353_0.png)
![](img/66c45bbed85bb7ba7f7b05dff49b5060_353_1.png)
![](img/66c45bbed85bb7ba7f7b05dff49b5060_353_2.png)

Figure 14.23. Left: The figure illustrates the environment mapping process for mapping the blue geometry enclosed in the spherical environment map. Q is the point mapped at P on the object. Middle: This shows a torus mapped using the cubic environment map in Figure 14.22. Right: A wine glass mapped using the spherical map in Figure 14.22.

However, since we do not do an accurate environment map computation we do miss out on some effects. For example, we cannot see self-reflections, a very common phenomenon in reflective objects as in the reflection of a spout or a handle of a teapot off the surface of the teapot. So, environment mapping creates a compelling realism via only a rudimentary approximation of the real phenomena. But such anomalies may go unnoticed to a few, such as a gamer in interactive gaming applications.

## 14.7 Transparency

So far, we have only considered rendering opaque objects. However, we encounter a large number of materials in the real world which are transparent or translucent (e.g. glass, liquids). In order to achieve interactive rendering of such objects, we introduce the concept of alpha blending. For this, we introduce a new channel of attributes in addition to the 3-channel RGB color. This is called the alpha channel, A. The alpha value A allows a rendering application to have a fractional contribution of the color from a source pixel S (i.e. the color of the pixel that is being rendered) blended with a fractional contribution from the destination pixel D (i.e. the color already existing in the framebuffer at that pixel). Let the color at S and D be (s_r, s_g, s_b, s_a) and (d_r, d_g, d_b, d_a) respectively, where s_a and d_a are values of the alpha channel. Note that prior to the introduction of the alpha channel, we assumed that the new value at the destination pixel D' = S, i.e. the new source color replaces the destination color.

However, in alpha blending, we adopt a more general way to achieve D' as a combination of D and S given by

```
D' = f_s(s_a, d_a) S + f_d(s_a, d_a) D
```

where f_s and f_d provide fractional values between 0 and 1. Note that the above equation is general and can be used to achieve a large variety of effects by different choices of f_s and f_d. For the particular case of transparency or translucency, the functions we use are

```
D' = s_a S + (1 - s_a) D.
```

Therefore, if the pixel being rendered is transparent, s_a = 0, achieving D' = D, i.e. the destination pixel will not change color at all since the source pixel is transparent. If the source pixel is opaque, as we have been assuming so long, then s_a = 1. Therefore, D' = S, i.e. the destination pixel gets overwritten by the color of the source pixel. If s_a is any other fraction between 0 and 1, we would get a combination of the source and destination colors to create the effect of translucency. Figure 14.24 shows the concept. Assume the egg to be the source and chicken to be the destination. The images from left to right are achieved with the above functions for transparency using s_a = 0, 0.5 and 1 respectively. It should also be noted that the order in which the translucent objects are drawn also determines the final color. Let O1 and O2 be two objects with alpha values s1 and s2 respectively. Let B be the background color to start with. If O1 is drawn first and then O2, then the final color will be O2 s2 + (1 - s2)(O1 s1 + (1 - s1) B). If the order is reversed, then the final color using the same blending function will be O1 s1 + (1 - s1)(O2 s2 + (1 - s2) B). Obviously, these two might result in different colors.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_354_0.png)

Figure 14.24. This figure shows the effect of alpha channel blending. Left: Chicken=1, Egg=0; Middle: Chicken = Egg = 0.5; Right: Chicken=0, Egg=1.

However, to achieve translucency correctly, there is depth to be considered. Only alpha channel manipulation will not work. Let us consider the following scenarios in Figure 14.25 to illustrate this. Consider the image plane shown by the horizontal line and the line of sight shown by the vertical dashed line. Three objects are shown. A is opaque while B and C are translucent. Their order of rendering is shown by the numbers on the right. In the first case (left), B will be rendered first and then its color will get attenuated by the alpha value of C, s_c. However, next the attenuated color will be completely replaced by the color of opaque A. However, physically since B and C are in front of A, we should see a combination of colors of all of A, B and C. Therefore, the result is wrong. In the second case (right), A will be rendered. Following this, during rendering of C, the framebuffer will be attenuated based on the alpha of C, s_c, and then again

prevent the back facing primitives from going through the rendering pipeline. Back face culling is a technique by which we detect such back facing polygons and remove them from using up computational resources to go through the model, view and projection transformations.

### Put a Face to the Name

Jim Blinn, a retired scientist, educator and industrial legend, is considered as one of the father figures of computer graphics (CG), in particular in light-matter interaction. He is the first person to introduce concepts of bump and reflection mapping which provided a very powerful tool to early computer graphics animators. Though the shading model using normal interpolation goes by the Phong shading model, it should be more accurately called the Blinn-Phong shading model since Blinn worked together with Phong on this model. Blinn was born in 1949 and received his bachelor's degree from University of Michigan in 1970. He received his PhD from University of Utah in 1978. He first became widely known for his work as a computer graphics expert at NASA's Jet Propulsion Laboratory (JPL), particularly for his work on computer graphics animations for various space missions to Jupiter, Saturn and Uranus, especially the Voyager project. These animations were shown on many news broadcasts as part of the press coverage of the missions and were the first exposure to computer animation for many people in the industry today. He is also known in the computer graphics community for his enthusiastic and inspirational role as an educator, mentor and a visionary. His columns "Jim Blinn's Corner" (today published as a book by Morgan Kaufmann) have inspired many to take computer graphics as their calling. These were articles, covering math, graphics pipelines and a wealth of tips and tricks which always kept graduate students motivated to work on the next big thing. He is well known for creating animation for three television education series: Carl Sagan's Cosmos: A Personal Voyage; Project MATHEMATICS!; and the pioneering instructional graphics in The Mechanical Universe. His talks in CG venues are still very popular due to his reputation of throwing a challenge to the community. In 1998, in a keynote talk in SIGGRAPH (the premier CG conference) he asked the CG community "to figure out how to drop a piece of spaghetti onto the plate and how it squiggles up and model the sauce on there for the frictional coefficients and so forth". This led to a large amount of research finally resulting in accurate CG simulations of protein foldings.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_357_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_358_0.png)

Figure 14.28. The figure shows back face culling in action in wire frame rendering of a cylinder (left) and torus (right). For each, you see the model rendering without back face culling on the left and with back face culling from the same or different viewpoint on the right.

To achieve this we can apply a very simple test. Note that any front facing primitive will have a normal vector whose angle with the view direction (from the vertex to the view point) will be within −90 to +90 degrees, i.e. its cosine is positive. The sign of the cosine can be computed using N.V, where N is the normal to the plane of the triangle and V is the view direction. Therefore, if this dot product is greater than 0, then these primitives should be rendered, otherwise they are discarded. This process is called back-face culling. Obviously, back-face culling cannot be used with transparent and translucent objects. Figure 14.28 illustrates the process of back face culling.

## 14.10 Visibility Culling

When we navigate a scene, usually the view frustum has a limited horizontal and vertical field of view. Therefore, objects which are not within this view frustum (e.g. objects behind us) are invisible and we should not spend resources to render those objects. Therefore, instead of making these objects go through the entire pipeline and be culled away in the last stage of clipping, the performance can be improved tremendously if objects which are not inside the view frustum are culled away very early in the pipeline. This process is called view frustum culling and is illustrated in Figure 14.29. Only the objects within the frustum or which intersect the frustum are rendered. The purple torus intersects the view frustum though it is only partially inside the frustum. Such objects are special cases and are handled appropriately. In the next few sections, we will introduce methods for achieving view-frustum culling with wireframe objects that show exactly the triangles that are rendered and those that are culled.

### 14.10.1 Bounding Volumes

The first method consists of defining a simple bounding volume around each object in the scene - e.g. a cube or a sphere. This bounding volume should be
