![](bbox=[0.2, 0.13, 0.72, 0.25])

Figure 7.8. The left three images show the effect of the focal length on the depth of field. Note that as the focal length increases the depth of field also increases. The right three images show the same effect for a smaller aperture. Note that for the same focal length, the smaller aperture have larger depth of field.

the aperture of the camera is reduced in size. Since c_z is directly proportional to aperture, the size of the circle of confusion goes down with reduced aperture. The implication of this is that if the pixel size remains the same, points at greater distance from f can now produce circle of confusion within p and therefore the depth of field of the camera will increase. This is also consistent with the pinhole camera model since as the aperture goes towards 0 as is the case in pinhole camera, the depth of field goes towards infinity. Usually aperture is expressed as a fraction of the focal length. An f2 aperture means an aperture size of f/2. These are usually specified as f-numbers. Typical f-numbers are f2, f4, f8, f16, f2.8, f5.6, f11 and so on. Figure 7.6 shows this effect.

Now, lets see what happens when the focal length of the lens is changed. With decrease in focal length, the 1/f term in Equation 7.35 increases thereby increasing c_z. Therefore, the depth of field of the camera reduces. This effect is shown in Figure 7.8. It also illustrates the combined effect of focal length and aperture on the depth of field.

![](bbox=[0.2, 0.6, 0.42, 0.75])

The change of the focal length also has an effect on the field of view captured by the camera. The longer the focal length, the smaller the field of view. To understand this, let us go back to the pinhole camera as shown in Figure 7.9. Let the image plane be moved at different focal lengths, f1, f2 and f3 such that f1 < f2 < f3. Therefore, if the sensor size remains constant, as the focal length increases the field of view - the angle between the lines passing from the center of projection through the extremities of the sensor - decreases. This effect makes the relative size of the flowers in 7.8 become bigger as the focal length increases.

Figure 7.9. This figure illustrates the effect of focal length on the field of view if the sensor size remains the same.