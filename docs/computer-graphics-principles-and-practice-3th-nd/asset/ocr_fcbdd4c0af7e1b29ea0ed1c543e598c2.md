# 13.3 Perspective Camera Specification

The WPF camera specification uses six parameters to specify a camera: position (a point), look direction and up direction (two vectors), near-plane distance and far-plane distance (two scalars), and field of view (an angle in degrees).

> > Why don’t we just render everything we can see? Our field of view is about 180°. Even if you say, “Sure, I can detect stuff in my peripheral vision, but I really *see* stuff within about a 120° view, sort of a cone extending in front of my eyes,” you’ll find that if you specify a 120° field of view, your pictures will look peculiar and distorted. That’s partly because we tend to view pictures so that they occupy a relatively small portion of our field of view. A computer monitor at a comfortable viewing distance may represent only a 25° field of view, for instance, while your cell-phone screen may be just a few degrees wide.
> >
> > If we *do* make a wide-angle picture and then display it in a way that makes the image occupy a large portion of our field of view, the results can seem less distorted, but there’s some evidence that even this doesn’t give the viewer a completely satisfactory sense of “seeing everything” [Koe11].
> >
> > So we compromise and take the approach used by photographers: We render only a modest portion of the eye’s field of view.

Figure 13.2 shows these. You can think of the camera being specified as a pinhole camera so that all rays entering the camera do so through a single point, specified as the **position** of the camera. You could also think of this as the center of the camera lens in a more conventional camera. In setting up a real-world photograph, we generally establish several things: the camera position, its orientation, and the field of view (often adjusted with a zoom control on the camera). For fancier cameras, we may also be able to adjust the **focal distance** (the distance to the points that are most in focus in the image), the **depth of field** (how far in front of and behind the focal distance things will be in focus), and even the tilt and offset of the camera lens relative to the camera body. The WPF specification, and that of most basic graphics systems, omits these latter aspects, since an ideal pinhole camera is in focus at all depths, and the pinhole is typically centered over the film or imaging sensor. We’ll return to these topics in Section 13.9.

![](bbox=[0.148, 0.707, 0.541, 0.902])

*Figure 13.2: The parts of a WPF camera specification.*