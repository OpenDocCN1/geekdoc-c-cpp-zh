# 106 Volodymyr V. Ivanchenko

![](bbox=[0.101, 0.083, 0.899, 0.362])

and provides a reasonable way to interpolate information along the surface. The only image regions where smoothness constraint is usually not enforced correspond to borders of objects; but those areas typically have high-contrast pixels with strong cues and thus are not affected by propagation. Thus, a cue conflict theory seems to be applicable to at least one computer vision problem where it facilitates information propagation and the creation of dense stereo maps from sparse cues.

Figure 5.2 shows 3D reconstruction of a surface region based on the above described flattening method. Note that reconstructed surfaces are dense and have no holes that are typical for a correlation-based stereo. It was possible to run a BP algorithm in near real time (less than 200 ms on GPU) with VGA image resolution and 32 disparity levels (Ivanchenko, Shen, and Coughlan, 2009).

We reconstructed a distant image region on purpose because the strength of a disparity cue decreases with the viewing distance. This makes distant regions good candidates for observing weak cues and for analyzing the role of a smoothness constraint that increases when a cue strength decreases. Note that this constraint describes properties of visual surfaces in the world as opposed to a mixture of priors that describes properties of the images.