
![](img/1274306e378c42ed8a0ad5669902d2a1_52_0.png)

Figure 2.7. The height plot in (b) is drawn on top of the current screen contents in (a) with additive blending to obtain the half-transparent plot result in (c). A black background is used.

In OpenGL, a large class of transparency-related effects can be achieved by using a special graphics mode called blending. To use blending, we must first enable it using the following function call:

```
glEnable(GL_BLEND);
```

Once blending is enabled, OpenGL will combine the pixels of every drawn primitive, such as polygons or lines, with the current values of the frame buffer (displayed image) at the locations drawn. In OpenGL terminology, the drawn primitive is called the source, whereas the frame buffer the primitive is drawn on is called the destination. Blending is performed independently for every source pixel drawn on a destination. If we denote the colors of the source and destination pixels by src and dst, respectively, the final value dst' of the destination pixel is given by the expression

```
dst' = sf * src + df * dst. (2.9)
```

Equation (2.9) is essentially a weighted combination of the source and destination colors using the source and destination weight factors sf and df respectively, which are both real values in the range [0, 1]. This equation is applied independently for every color component (R, G, and B). The weights sf and df, also called blending factors, can be specified in a variety of ways. In the following, we show how to specify these factors to achieve a simple transparency effect that combines the grid and plot rendering in our height-plot example. The final result is shown in Figure 2.7(c). To obtain this result, we proceed as follows. First, we clear the screen to black. The reason for using black instead of the usual white background will become apparent soon. The frame buffer is cleared by the following sequence of OpenGL calls:

```
glClearColor(0.0, 0.0, 0.0); //specify the clear color
glClear(GL_COLOR_BUFFER_BIT); //clear the frame buffer
```

Next, we draw the grid structure. We do not use any blending, since we want the grid itself to be fully opaque. The result is shown in Figure 2.7(a). The final step is to draw the half-transparent height plot on top of this grid. The height plot to be drawn is shown, without the actual transparency, in Figure 2.7(b). For this, we first enable blending, as described previously. Next, we specify the blending factors $s_f$ and $d_f$. A half-transparent plot is achieved by using a source factor $s_f < 1$. To ensure that, at each pixel, the contribution of the grid and plot objects sums up to one, we use a destination factor $d_f = 1 - s_f$. This combination is achieved by the OpenGL code

```
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
glColor4f(r,g,b,s_f);
```

For the result shown in Figure 2.7(c), the colors $r,g,b$ have the same values as for the example discussed in Section 2.3 and $s_f$ has a value of 0.7.

The function glBlendFunc takes two parameters that specify the source and destination blending factors. These parameters are symbolic constants rather than being the blending factors themselves, and specify how the actual blending factors $s_f$ and $d_f$ will be computed. The most commonly used values of these constants are as follows. The constant GL_ONE sets the value of the respective blending factor to 1. The constant GL_SRC_ALPHA specifies that the source factor $s_f$ will be taken from the fourth component, also called the alpha component, of the color of the drawn primitive. Hence, if we next set the color using glColor4f(r, g, b, s_f), $s_f$ will be the actual source blending factor used. The constant GL_ONE_MINUS_SRC_ALPHA sets the respective blending factor to $1 - s_f$, where $s_f$ is the alpha value of the drawn primitives, as specified previously.

These parameters allow us to obtain various transparency effects. Using glBlendFunc(GL_SRC_ALPHA, GL_ONE) followed by drawing primitives that have the desired alpha values set via glColor4f starting with a black frame buffer effectively adds up the primitives' colors, weighted by their respective alpha values. We can achieve the same effect by using glBlendFunc(GL_ONE, GL_ONE), i.e., setting $s_f = d_f = 1$, and factoring the source blending factor in the color by using glColor3f(rs_f, gs_f, bs_f). Using glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA) realizes the convex combination

![](img/1274306e378c42ed8a0ad5669902d2a1_54_0.png)

Figure 2.8. The height plot drawn half-transparently on top of the domain grid using a white background.

```
dst' = s_f * src + (1 - s_f) * dst.
```

The value of dst' is always clamped to one by OpenGL, so it is a good idea to use blending factors that will sum up to one when all primitives are drawn. This is achieved automatically if we use the blending functions as set by the convex combination in Equation (2.10).

Finally, there is a fourth constant GL_ZERO, which sets the respective source or destination blending factor to zero. Hence, calling the glBlendFunc(GL_ONE, GL_ZERO) function is equivalent to having blending disabled, i.e., the source color will simply overwrite the destination (frame buffer) color.

Figure 2.8 shows the height plot drawn with the same transparency value of 0.7 on top of the domain grid, this time using a white background, obtained by setting glClearColor(1,1,1,0). We leave the construction of the actual OpenGL blending code that achieves this image as an exercise for the reader.

Besides transparency, blending can be used to obtain many other graphical effects that are useful in visualization applications. Volume visualization, described in Chapter 10, fundamentally relies on blending to display volumetric datasets. Another use of blending is demonstrated in Section 6.6, for the construction of animated flow textures for visualizing vector fields. Yet another application of blending is described in Section 9.4.5, for the computation of distance fields in image data.

## 2.6 Viewing

All images of our height plot shown so far display the plot as viewed from a certain angle and position in space. To understand how to specify such viewing parameters, we need to understand how OpenGL processes 3D vertex coordinates to create the final image displayed on the screen. This process has several steps, or transforms, which are described next.

Virtual camera. The first step in specifying how to view a 3D scene is to specify where from, and in which direction, we want to look at the scene. The easiest way to picture this is to imagine that we have a virtual photo camera that we want to point at the scene in a specific way. In OpenGL, such a camera can be specified by indicating its location (also called the eye position e), a location towards which the camera is pointing (also called the center position c), and a vector u indicating how the camera is rotated around the viewing direction c - e (also called the “up” vector). Figure 2.9 illustrates this. The plane orthogonal to the viewing direction, on which the final image will appear, is also called the view plane.

![](img/1274306e378c42ed8a0ad5669902d2a1_55_0.png)

Figure 2.9. Extrinsic parameters of the OpenGL camera.

In OpenGL, specifying the eye, center, and up vector values for a camera can be done using the gluLookAt function²

```
glMatrixMode (GL_MODELVIEW);
glLoadIdentity ();
gluLookAt (ex, ey, ez, cx, cy, cz, ux, uy, uz)
```

The first two function calls (glMatrixMode and glLoadIdentity) ensure that the subsequent gluLookAt call will modify the extrinsic camera parameters of OpenGL, rather than intrinsic camera parameters, which are discussed in the next section. Extrinsic camera parameters are also called modelview parameters in OpenGL, hence the name GL_MODELVIEW. The up vector u should not be parallel to the viewing direction c - e, otherwise we cannot unambiguously define the view plane. A simple but effective default setting is to have c equal to the center of the viewed scene, i.e., the average of all vertex coordinates; u equal to the y-axis of the 3D space, i.e., u = (0, 1, 0); and e at a distance from c slightly larger than the size of the scene's bounding-box. All three vectors e, c, and u are given in the same coordinate system as the 3D scene to view. These values are also known as the extrinsic camera parameters, since they do not specify how the camera is actually constructed, but only its placement in the 3D space.

Projection. After placing the camera in 3D space, we need to specify how the camera itself operates, or its intrinsic parameters. Following the analogy with a physical photo camera, which captures perspective projections of a 3D scene on a planar surface, intrinsic parameters give the focal length, field-of-view, and aspect ratio of the view area where we wish to capture the image (Figure 2.10). This view area is a rectangle in the view plane whose center is on the view direction line c - e and whose axes are parallel to u, respectively (c - e) × u. The focal length znear gives the distance, along the view direction, from the eye position e to the view plane. No objects closer to e than znear are “seen” by the camera. Hence, the view plane is also called the near clipping plane, as it clips, or removes from viewing, objects in front of it. The field-of-view fov is the angle formed by the top, respective bottom, borders of the view area with the eye position e. The aspect ratio aspect gives the ratio of the horizontal to the vertical size of the view area. Finally, the value zfar gives the distance, along the view direction, from the eye position e to a plane parallel to, and behind, the

2. Strictly speaking, gluLookAt and all other functions discussed next that start with glu are part of the Graphics Library Utility (GLU) library and OpenGL. As virtually any system which offers OpenGL also offers GLU, we do not make this distinction next.
