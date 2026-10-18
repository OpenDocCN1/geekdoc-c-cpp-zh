![](bbox=[0.12, 0.1, 0.82, 0.38])

# FIGURE 12.6: Flowchart of typical AVSR systems.

# 12.3.2.1 Visual Front End

The visual front end consists of a two-stage processing of the images. First, pose normalization is needed to extract the region of interest from facial images. Typically, the mouth region is highly correlated to speech. Then, the normalized images are further transformed into the desired feature representation. In the literature, a large variety of image processing and computer vision methods have been applied in the visual front end for AVSR. Some examples are face/mouth/lips detection and tracking, shape and appearance modeling for face/mouth, and global/local image features. The diversity of front end methods increase the difficulty in comparing different AVSR systems. So far, no single method has been proven to be strictly superior to others.

# Normalization

Most pose normalization methods in AVSR extract lips from the image. The algorithms for lips localization mainly fall into two categories [76]. The first category makes use of the prior information about the whole face. Two representative methods are active shape model (ASM) and active appearance model (AAM) [19]. While the ASM represents the face as a set of landmarks, AAM further includes the textures inside the face boundary. These methods can be extended to 3D [24] to further normalize the out-of-plane head rotations. The other category only uses the local appearance around the lips [1]. The informative aspects of lips are the shape of outer and inner contours, and the image appearance inside the contours. Existing AVSR front ends can be shape-based [56], appearance-based (pixel) [61], or a combination of the two.

Robust pose normalization and part detection are, in general, difficult tasks. This is especially true in uncontrolled environments with varying illumination and background. Most of the current AVSR research simplifies the normalization stage by controlled environment and human labeling. For example, many audio visual speech corpora are recorded in limited pose variation and constant lighting settings [66]. The cropping window for mouth regions is usu-