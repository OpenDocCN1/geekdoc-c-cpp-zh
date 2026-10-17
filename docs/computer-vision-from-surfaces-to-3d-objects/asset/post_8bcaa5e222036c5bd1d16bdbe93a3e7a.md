
The efficient belief propagation techniques we developed have similar applications in a variety of perceptual inference tasks. These and other statistical inference techniques promise to significantly advance the state of the art in computer vision and to improve our understanding of perceptual inference in general.

In addition to improved performance, the approach to shape from shading described above offers a new degree of flexibility that should allow shading to be exploited in more general and realistic scenarios. Previous approaches to shape from shading typically relied heavily on the exact nature of the Lambertian reflectance equations, and so could only be applied to surfaces with specific (i.e., matte) reflectance qualities with no surface markings. Also, specific lighting conditions were assumed. The approach described above applies directly to a statistical model of the relationship between shape and shading, and so it does not depend on the exact nature of the Lambertian equation or specific lighting arrangements. Also, the efficient higher-order belief propagation techniques described here make it possible to exploit stronger, nonpairwise models of the prior probability of 3D shapes. Because the problem of depth inference is so highly underconstrained, and natural images admit large numbers of plausible 3D interpretations, it is crucial to utilize an accurate model of the prior probability of 3D surface. Knowing what 3D shapes commonly occur in nature and what shapes are *a priori* unlikely or odd is a very important constraint for depth inference. Finally, the factor graph representation of the shape-from-shading problem (see Figure 1.6) can be generalized naturally to exploit other depth cues, such as occlusion contours, texture, perspective, or the da Vinci correlation and shadow cues. The state-of-the-art approaches to the inference of depth from binocular stereo pairs typically employ belief propagation over a MRF. These approaches can be combined with our shape-from-shading framework in a fairly straightforward way, allowing both shading and stereo cues to be simultaneously utilized in a statistically optimal way. Statistical approaches to depth inference make it possible to work toward a more unified and robust depth inference framework, which is likely to become a major area of future vision research.

## ACKNOWLEDGMENTS

This work was supported by NSF CISE IIS 0713206 and AFOSR FA9550-09-1-0678 to T. S. Lee, and an NSF Graduate Research Fellowship to B. Potetz.

## Active Segmentation: A New Approach

Ajay Mishra
Yiannis Aloimonos

- 2.1 Introduction 26
- 2.2 Background 29
  - 2.2.1 Image Segmentation 30
    - 2.2.1.1 Region-Based Methods 30
    - 2.2.1.2 Contour-Based Methods 31
  - 2.2.2 Motion Segmentation 32
- 2.3 Fixation-Based Segmentation 33
  - 2.3.1 Computing Probabilistic Boundary Edge Map 34
  - 2.3.2 Why Polar? 36
  - 2.3.3 Finding the Optimal Contour 38
    - 2.3.3.1 Cartesian to Polar Edge Map 38
    - 2.3.3.2 Finding the Optimal Cut through the Polar Edge Map: An Inside versus Outside Segmentation 40
- 2.4 Results 42
- 2.5 Fixation Strategy 46
  - 2.5.1 Stability Analysis 47
- 2.6 Conclusion 49

### 2.1 INTRODUCTION

Segmenting a scene (or image) into regions is an important step in visual processing. The regions are more discriminative than the individual pixels and fewer in number than the total number of pixels. This makes regions better suited and computationally less expensive to use for high-level visual processing like tracking, recognizing objects, and three-dimensional (3D) reconstruction. But to make segmentation an essential first step of vision algorithms, the segmentation algorithm needs to be consistent in its output and should not require any user input.

Let us give a state-of-the-art example to explain what it means for a segmentation algorithm to be fully automatic and consistent. We consider only a single image here shown in Figure 2.1a, but our analysis is not restricted to single images only. Most segmentation algorithms amount to statistical optimization procedures that require an estimate of the number of regions either directly or indirectly (in terms of other thresholds) to segment the scene. Figure 2.1b,c are the segmentation of Figure 2.1a using (Shi and Malik, 2000) with its parameter (number of regions) set to 10 and 60, respectively. If the trees in the scene are of interest, Figure 2.1b is more meaningful than Figure 2.1c, wherein the tree has been oversegmented into a large number of small regions. Such segmentation is termed *oversegmentation* because the region of interest is split into many small regions. However, if the tiny horse in Figure 2.1a is of interest, then Figure 2.1c is more meaningful, as the horse appears as a combination of just two regions in the image. The segmentation in Figure 2.1b, on the other hand, does not even have the region corresponding to the horse. It is a case of undersegmentation, wherein small regions are merged to form bigger regions. Depending upon which is an important region and at what scale it exists, the appropriate parameter needs to be set for (Shi and Malik, 2000) to output a meaningful segmentation.

![](img/4d808358747f9096d24f831e5f9d8083_49_0.png)
![](img/4d808358747f9096d24f831e5f9d8083_49_1.png)

(a) (b)

![](img/4d808358747f9096d24f831e5f9d8083_49_2.png)

(c)

**FIGURE 2.1** *(See color insert following p. 94.)* Segmentation results by Jianbo Shi and Jitendra Malik (2000) for the image (a) for the two cases when the number of regions is chosen to be 10 and 60, as shown in (b) and (c), respectively. If the trees are the object of interest, the segmentation in (b) is suitable, whereas if the horse is of interest, then the segmentation given in (c) is more suitable.

But, in a real scene, there can be multiple regions of interest in the scene, and they can exist at dramatically different scales, as is the case in this example. So, a consistent and automatic segmentation algorithm is that which can segment the region of interest irrespective of its size in the image.

Such a segmentation is associated with the region of interest. Unlike the current algorithms, it will only segment the region of interest as foreground and everything else in the scene as background. In fact, we know that the human (primate) visual system works in a similar way. It observes and makes sense of a dynamic scene (video) or static scene (image) by making a series of fixations at various salient locations in the scene. Researchers have studied in great length about where the human eye fixates (Cerf et al., 2008; Walther and Koch, 2006), but little is known about the operations carried out in the human visual system during a fixation. It is also well known that the structure of the human retina is such that only the small neighborhood around these fixations is captured in high resolution by the fovea, while the rest of the scene is captured in lower resolution by the sensors on the periphery of the retina. We suggest that, as a first step, the visual system segments the region on which it is fixating. Rather than segmenting the entire scene or image at once, we suggest the human visual system segments the scene in terms of individual regions for each of the fixations in the scene. For example, as the attention of the visual system is drawn to the horse (Figure 2.2a), it segments the horse (Figure 2.2b). When the attention is drawn to the trees (Figure 2.2c), it segments the trees (Figure 2.2d).

Another important factor in designing a segmentation algorithm is how it uses the visual cues to find the region. There are two types of visual cues: monocular cues (namely, intensity, color, and texture) that come from a single image only, binocular cues (such as depth), and motion cues that are calculated by using two or more images of the scene. Usually, the existing segmentation algorithms handle either of these two types of cues. Most importantly, the basic framework changes significantly from the image segmentation algorithms that use only monocular cues to the motion segmentation algorithms that use motion cues to segment the region in the image. Instead, the framework of the desired segmentation algorithm should be cue independent, meaning the method to find the region should not change if we just have monocular cues to the case when color, texture, depth, and motion cues are all available.

In this chapter, we formulate the problem of segmentation such that it incorporates all available cues to segment the region of interest being fixated at. Our
