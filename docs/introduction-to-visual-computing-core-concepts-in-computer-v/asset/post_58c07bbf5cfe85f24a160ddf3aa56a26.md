
![](img/66c45bbed85bb7ba7f7b05dff49b5060_186_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_186_1.png)

Figure 7.7. Top: This shows the effect of reducing the aperture size on the circle of confusion. The bold line shows the original aperture in Figure 7.5 and the dotted line shows the effect of reducing the aperture size that reduces the circle of confusion. Bottom: This shows some images taken from a camera using varying apertures decreasing from left to right.

by $c_z$. Using thin lens equation, it can be shown that

```
$$c_z = a r \left( \frac{1}{f} - \frac{1}{z} \right), \qquad (7.35)$$
```

where $a$ is the aperture of the lens. If $c_z$ is less than the size of the pixel $p$, the image will look focused. The range of depth for which $c_z < p$ can be shown to be from $(f - d)$ to $(f + d)$ where $d = \frac{p f^2}{p f - a r}$. This range of depth from $f - d$ to $f + d$ is called the depth of field of the camera.

Next, let us see how these different parameters like aperture and focus have an effect on the picture captured by a camera. First let us check what happens when

![](img/66c45bbed85bb7ba7f7b05dff49b5060_187_0.png)

Figure 7.8. The left three images show the effect of the focal length on the depth of field. Note that as the focal length increases the depth of field also increases. The right three images show the same effect for a smaller aperture. Note that for the same focal length, the smaller aperture have larger depth of field.

the aperture of the camera is reduced in size. Since c_z is directly proportional to aperture, the size of the circle of confusion goes down with reduced aperture. The implication of this is that if the pixel size remains the same, points at greater distance from f can now produce circle of confusion within p and therefore the depth of field of the camera will increase. This is also consistent with the pinhole camera model since as the aperture goes towards 0 as is the case in pinhole camera, the depth of field goes towards infinity. Usually aperture is expressed as a fraction of the focal length. An f2 aperture means an aperture size of f/2. These are usually specified as f-numbers. Typical f-numbers are f2, f4, f8, f16, f2.8, f5.6, f11 and so on. Figure 7.6 shows this effect.

Now, lets see what happens when the focal length of the lens is changed. With decrease in focal length, the 1/f term in Equation 7.35 increases thereby increasing c_z. Therefore, the depth of field of the camera reduces. This effect is shown in Figure 7.8. It also illustrates the combined effect of focal length and aperture on the depth of field.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_187_1.png)

The change of the focal length also has an effect on the field of view captured by the camera. The longer the focal length, the smaller the field of view. To understand this, let us go back to the pinhole camera as shown in Figure 7.9. Let the image plane be moved at different focal lengths, f1, f2 and f3 such that f1 < f2 < f3. Therefore, if the sensor size remains constant, as the focal length increases the field of view - the angle between the lines passing from the center of projection through the extremities of the sensor - decreases. This effect makes the relative size of the flowers in 7.8 become bigger as the focal length increases.

Figure 7.9. This figure illustrates the effect of focal length on the field of view if the sensor size remains the same.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_188_0.png)

Figure 7.10. This figure illustrates motion blur. The color wheel in the left is static and its motion increases in the following figures from left to right, the rightmost one being the fastest. The picture is taken with the same shutter speed creating more blur for faster motion.

Finally, we will discuss one more parameter of a practical camera, the shutter speed. The sensor in the camera needs to be exposed for a limited time to capture the image. This exposure time is controlled by the shutter. When you hear a camera ‘click’, the shutter opens and remains so for sometime exposing the sensor to the light and then closes.

The time the shutter is open has a linear effect on the amount of light that is let in. Usually the shutter is open for a fraction of a second (e.g. 1/30, 1/60). If any object in the scene moves during the time the shutter is open, the image of the object is captured at multiple locations creating an effect called the motion blur as shown in Figure 7.10.

## 7.3 Conclusion

In this chapter we covered the fundamental model of a pinhole camera and its application in 3D depth reconstruction and homography based modeling. A more mathematical treatise of this model is available in [Faugeras 93], the classical book on 3D computer vision. More about stereo reconstruction and camera calibration is available at [Szeliski 10]. Details about the practical camera can be explored further by taking a course on computational photography – [Lukac 10] offers a in depth treatise in this direction.

## Bibliography

[Faugeras 93] Olivier Faugeras. Three-dimensional Computer Vision: A Geometric Viewpoint. MIT Press, 1993.

[Lukac 10] Rastislav Lukac. Computational Photography: Methods and Applications, First edition. CRC Press, Inc., 2010.

[Szeliski 10] Richard Szeliski. Computer Vision: Algorithms and Applications. Springer-Verlag New York, Inc., 2010.

## Summary: Do you know these concepts?

- Pinhole Camera
- Intrinsic and Extrinsic Camera Parameters
- Camera Calibration
- Depth Estimation or Reconstruction
- Stereo Camera Pair
- Homography
- Focal Length
- Aperture
- Depth of Field
- Shutter Speed
- Motion Blur
- Field of View

## Exercises

1. Consider the following 3 × 4 camera matrix

$$C = \begin{pmatrix} 10 & 2 & 11 & 19 \\ 10 & 5 & 10 & 50 \\ 5 & 14 & 2 & 17 \end{pmatrix} \tag{7.36}$$

Consider the 3D point in homogeneous coordinates $X = (0, 2, 2, 1)^T$.

+   (a) What are the Cartesian coordinates of the point X in 3D?
+   (b) What are the Cartesian image coordinates of the projection of X?

2. Consider an ideal pinhole camera with focal length of 5mm. Each pixel is 0.02mm × 0.02mm and the image principal point is at pixel (500, 500). Pixel coordinates start at (0, 0) in the upper-left corner of the image.

+   (a) What is the 3 × 3 camera calibration matrix, K, for this camera configuration?
+   (b) Assuming the world coordinate frame is aligned with the camera coordinate frame (i.e., their origins are the same and their axes are aligned), and the origins are at the cameras pinhole, what is the 3 × 4 matrix that represents the extrinsic, rigid body transformation between the camera coordinate system and the world coordinate system?
+   (c) Combining your results from the previous two questions, compute the projection of scene point (100, 150, 800) into image coordinates.

3. A camera is rigidly mounted so that it views a planar table top. A projector is also rigidly mounted above the table and projects a narrow beam of light onto the table, which is visible as a point in the image of the table top. The height of the table top is precisely controllable but otherwise the positions of the camera, projector, and table are unknown. For table top heights of 50mm and 100mm, the point of light on the table is detected at image pixel coordinates (100, 250) and (140, 340) respectively.

+   (a) Using a projective camera model specialized for this particular scenario, write a general formula that describes the relationship between world coordinates (x), specifying the height of the table top, and image coordinates (u, v), specifying the pixel coordinates where the point of light is detected. Give your answer using homogeneous coordinates and a projection matrix containing variables.
+   (b) For the first table top position given above and using your answer in the previous question, write out the explicit equations that are

generated by this one observation. How many degrees of freedom does this transformation have?

(c) How many table top positions and associated images are required to solve for all of the unknown parameters in the projective camera model?

(d) Once the camera is calibrated, given a new unknown height of the table and an associated image, can the height of the table be uniquely solved for? If so, give the equation(s) that is/are used. If not, describe briefly why not.

(e) If in each image we only measured the u pixel coordinate of the point of light, could the camera still be calibrated? If so, how many table top positions are required? If not, describe briefly why not.

4. Assume a camera with camera matrix $C = K[r_1 r_2 r_3 t]$, where $K$ is the intrinsic parameter matrix and $r_1$, $r_2$, and $r_3$ are the columns of the rotation matrix. Let $\pi$ be the XY plane at $Z = 0$. We know that any point $P$ in this plane can be related to the camera image point $P$ by a homography $H$, i.e. $P = H P$. Show that $H = K[r_1 r_2 t]$.

5. Consider a panoramic image generation application where the camera is placed on a tripod and rotated to capture multiple images for panoramic image generation. Can two adjacent images in this sequence be related by a homography? If so, under what conditions is this possible?

6. Four projectors are tiled in a $2 \times 2$ array to create a tiled display on a flat wall. The projectors have some overlap between each other. What is the minimum dimension of the matrix that relates pixel $(x, y)$ in one projector to a pixel $(x', y')$ in another. Justify your answer.

7. What are the two parameters in a practical camera that allow you to control the amount of light reaching the sensor? How does the elements or events of a scene guide the choice of which parameter you would use to control the amount of light?

8. Freezing motion is a technique to choose the correct shutter speed for capturing a moving object so that they appear to be static or frozen in the image. You are asked to freeze motion for a moving car, a person jogging in the park, a person taking a stroll on the beach, and a fast moving train. You are allowed to choose between four shutter speeds of $\frac{1}{125}$, $\frac{1}{250}$, $\frac{1}{500}$, and $\frac{1}{1000}$. Which speed will you choose for which object?

9. Consider a parametric line $P_0 + \alpha(P_1 - P_0)$ in the 3D scene. Consider a point $P$ moving on this line as $\alpha$ goes from 0 to 1. Show that its projection under the camera calibration matrix will converge to a vanishing point.
