
## 10.9 Another Example of Building a 2D Transformation

Suppose we want to find a 3 × 3 matrix transformation that rotates the entire plane 30° counterclockwise around the point P = (2, 4), as shown in Figure 10.14. As you’ll recall, WPF expresses this transformation via code like this:

```xml
<RotateTransform Angle="-30" CenterX="2" CenterY="4"/>
```

![](img/f464cd0043eb5336aa0543fe20a0561b_288_0.png)

*Figure 10.14:* We'd like to rotate the entire plane by 30° counter-clockwise about the point P = (2, 4).

An implementer of WPF then must create a matrix like the one we're about to build.

Here are two approaches.

First, we know how to rotate about the origin by 30°; we can use the transformation T1 from the start of the chapter. So we can do our desired transformation in three steps (see Figure 10.15).

- 1. Move the point (2, 4) to the origin.
- 2. Rotate by 30°.
- 3. Move the origin back to (2, 4).

The matrix that moves the point (2, 4) to the origin is

```text
[ 1  0 -2 ]
[ 0  1 -4 ]
[ 0  0  1 ]        (10.74)
```

The one that moves it back is similar, except that the 2 and 4 are not negated. And the rotation matrix (expressed in our new 3 × 3 format) is

```text
[ cos 30°  -sin 30°   0 ]
[ sin 30°   cos 30°   0 ]
[   0         0       1 ]        (10.75)
```

The matrix representing the entire sequence of transformations is therefore

```text
[ 1  0  2 ] [ cos 30°  -sin 30°   0 ] [ 1  0 -2 ]
[ 0  1  4 ] [ sin 30°   cos 30°   0 ] [ 0  1 -4 ]
[ 0  0  1 ] [   0         0       1 ] [ 0  0  1 ]        (10.76)
```

> **Inline Exercise 10.18:** (a) Explain why this is the correct order in which to multiply the transformations to get the desired result.  
> (b) Verify that the point (2, 4) is indeed left unmoved by multiplying [2 4 1]^T by the sequence of matrices above.

The second approach is again more automatic: We find three points whose target locations we know, just as we did with the windowing transformation above. We’ll use P = (2, 4), Q = (3, 4) (the point one unit to the right of P), and R = (2, 5) (the point one unit above P). We know that we want P sent to P, Q sent to (2 + cos 30°, 4 + sin 30°), and R sent to (2 − sin 30°, 4 + cos 30°). (Draw a picture to convince yourself that these are correct.) The matrix that achieves this is just

$$
\begin{bmatrix}
2 & 2+\cos30^\circ & 2-\sin30^\circ\\
4 & 4+\sin30^\circ & 4+\cos30^\circ\\
1 & 1 & 1
\end{bmatrix}
\begin{bmatrix}
2 & 3 & 2\\
4 & 4 & 5\\
1 & 1 & 1
\end{bmatrix}^{-1}. \qquad (10.77)
$$

Both approaches are reasonably easy to work with.

There’s a third approach—a variation of the second—in which we specify where we want to send a point and two vectors, rather than three points. In this case, we might say that we want the point $P$ to remain fixed, and the vectors $\mathbf e_1$ and $\mathbf e_2$ to go to

$$
\begin{bmatrix}
\cos30^\circ\\
\sin30^\circ\\
0
\end{bmatrix}
\quad \text{and} \quad
\begin{bmatrix}
-\sin30^\circ\\
\cos30^\circ\\
0
\end{bmatrix}, \qquad (10.78)
$$

respectively. In this case, instead of finding matrices that send the vectors $\mathbf e_1$, $\mathbf e_2$, and $\mathbf e_3$ to the desired three points, before and after, we find matrices that send those vectors to the desired point and two vectors, before and after. These matrices are

$$
\begin{bmatrix}
2&1&0\\
4&0&1\\
1&0&0
\end{bmatrix}
\quad \text{and} \quad
\begin{bmatrix}
2&\cos30^\circ&-\sin30^\circ\\
4&\sin30^\circ&\cos30^\circ\\
1&0&0
\end{bmatrix}, \qquad (10.79)
$$

so the overall matrix is

$$
\begin{bmatrix}
2&\cos30^\circ&-\sin30^\circ\\
4&\sin30^\circ&\cos30^\circ\\
1&0&0
\end{bmatrix}
\begin{bmatrix}
2&1&0\\
4&0&1\\
1&0&0
\end{bmatrix}^{-1}. \qquad (10.80)
$$

These general techniques can be applied to create any linear-plus-translation transformation of the $w=1$ plane, but there are some specific ones that are good to know. Rotation in the $xy$-plane, by an angle $\theta$ (rotating the positive $x$-axis toward the positive $y$-axis) is given by

$$
R_{xy}(\theta)=
\begin{bmatrix}
\cos\theta&-\sin\theta&0\\
\sin\theta&\cos\theta&0\\
0&0&1
\end{bmatrix}. \qquad (10.81)
$$

In some books and software packages, this is called rotation around $z$; we prefer the term “rotation in the $xy$-plane” because it also indicates the direction of rotation (from $x$, toward $y$). The other two standard rotations are

$$
R_{yz}(\theta)=
\begin{bmatrix}
1&0&0\\
0&\cos\theta&-\sin\theta\\
0&\sin\theta&\cos\theta
\end{bmatrix}. \qquad (10.82)
$$

and

$$
R_{zx}(\theta)=
\begin{bmatrix}
\cos\theta&0&\sin\theta\\
0&1&0\\
-\sin\theta&0&\cos\theta
\end{bmatrix}; \qquad (10.83)
$$

note that the last expression rotates $z$ toward $x$, and not the opposite. Using this naming convention helps keep the pattern of plusses and minuses symmetric.

![](img/f464cd0043eb5336aa0543fe20a0561b_289_0.png)

*Figure 10.15:* The house after translating $(2,4)$ to the origin, after rotating by $30^\circ$, and after translating the origin back to $(2,4)$.

Now the code begins like this:

```xml
<Canvas ...
    <Canvas.Resources>
        <ControlTemplate x:Key="ClockHandTemplate">
            <Polygon
                Points="0.3,-1   -0.2,8   0,9   0.2,8   0.3,-1"
                Fill="Navy"/>
        </ControlTemplate>
        <ControlTemplate x:Key="CircleTemplate">
            <Polygon
                Points="1,0   0.707,0.707   0,1   -0.707,0.707
                        -1,0   -0.707,-0.707   0,-1   0.707,-0.707"
                Fill="LightGray"/>
        </ControlTemplate>
    </Canvas.Resources>
```

This code defines the geometry that we'll use to create the face and hands of the clock. With this change, the circular clock face will be defined by transforming a template “circle” represented by eight evenly spaced points on the unit circle. This form of specification, although not idiomatic in WPF, is quite similar to scene specification in many other scene-graph packages.

The actual creation of the scene now includes building the clock face from the `CircleTemplate`, and building the hands as before.

```xml
<!-- 1. Background of the clock -->
<Control Name="Face"
         Template="{StaticResource CircleTemplate}">
    <Control.RenderTransform>
        <ScaleTransform ScaleX="10" ScaleY="10" />
    </Control.RenderTransform>
</Control>

<!-- 2. The minute hand -->
<Control Name="MinuteHand"
         Template="{StaticResource ClockHandTemplate}">
    <Control.RenderTransform>
        <TransformGroup>
            <RotateTransform Angle="180" />
            <RotateTransform x:Name="ActualTimeMinute" Angle="0" />
        </TransformGroup>
    </Control.RenderTransform>
</Control>

<!-- 3. The hour hand -->
<Control Name="HourHand" Template="{StaticResource ClockHandTemplate}">
    <Control.RenderTransform>
        <TransformGroup>
            <ScaleTransform ScaleX="1.7" ScaleY="0.7" />
            <RotateTransform Angle="180" />
            <RotateTransform x:Name="ActualTimeHour"
                             Angle="0" />
        </TransformGroup>
    </Control.RenderTransform>
</Control>
```

All that remains is the transformation from `Canvas` to WPF coordinates, and the timers for the animation, which set the `ActualTimeMinute` and `ActualTimeHour` values.

```xml
<Canvas.RenderTransform>
  ...same as before...
</Canvas.RenderTransform>

<Canvas.Triggers>
  <EventTrigger RoutedEvent="FrameworkElement.Loaded">
    <BeginStoryboard>
      <Storyboard>
        <DoubleAnimation
          Storyboard.TargetName="ActualTimeHour"
          Storyboard.TargetProperty="Angle"
          From="0.0" To="360.0"
          Duration="00:00:01.0" RepeatBehavior="Forever"
        />
        <DoubleAnimation
          Storyboard.TargetName="ActualTimeMinute"
          Storyboard.TargetProperty="Angle"
          From="0.0" To="4320.0"
          Duration="00:00:01.0" RepeatBehavior="Forever"
        />
      </Storyboard>
    </BeginStoryboard>
  </EventTrigger>
</Canvas.Triggers>

</Canvas>
```

As a starting point in transforming this scene description into an image, we’ll assume that we have a basic graphics library that, given an array of points representing a polygon, can draw that polygon. The points will be represented by a 3×k array of homogeneous coordinate triples, so the first column of the array will be the homogeneous coordinates of the first polygon point, etc.

We’ll now explain how we can go from something like the WPF description to a sequence of drawPolygon calls. First, let’s transform the XAML code into a tree structure, as shown in Figure 10.18, representing the scene graph (see Chapter 6).

We’ve drawn transformations as diamonds, geometry as blue boxes, and named parts as beige boxes. For the moment, we’ve omitted the matter of instancing of the ClockHandTemplate and pretended that we have two separate identical copies of the geometry for a clock hand. We’ve also drawn next to each transformation the matrix representation of the transformation. We’ve assumed that the angle in ActualTimeHour is 15° (whose cosine and sine are approximately 0.96 and 0.26, respectively) and the angle in ActualTimeMinute is 180° (i.e., the clock is showing 12:30).

> **Inline Exercise 10.19:** (a) Remembering that rotations in WPF are specified in degrees and that they rotate objects in a *clockwise* direction, check that the matrix given for the rotation of the hour hand by 15° is correct.  
> (b) If you found that the matrix was wrong, recall that in WPF x increases to the right and y increases *down*. Does this change your answer? By the way, if you ran this program in WPF and debugged it and printed the matrix, you’d find the negative sign on the (2, 1) entry instead of the (1, 2) entry. That’s because WPF internally uses row vectors to represent points, and multiplies them by transformation matrices on the right.
