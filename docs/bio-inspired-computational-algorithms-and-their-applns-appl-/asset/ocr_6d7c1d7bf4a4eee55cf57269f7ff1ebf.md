# 6. Conclusions

In this chapter, a database for visual and thermal images was created and several techniques were developed to improve image quality as an effort to address the illumination challenge in face recognition.

Firstly, one image enhancement algorithm was designed to improve the images' visual quality. Experimental results showed that the enhancement algorithm performed well and provided good results in terms of both luminance and contrast enhancement. In the luminance enhancement part, it has been shown that the proposed algorithm worked well for both dark and bright images. In the contrast enhancement part, it was proven that the proposed nonlinear transfer functions could make unseen or barely seen features in low contrast images clearly visible.

Secondly, the IR and enhanced visual images taken from different sensors, viewpoints, times and resolution were registered. A correspondence between an IR and a visual image was established based on a set of image features detected by the Harris Corner detection algorithm in both images. A spatial transformation matrix was determined based on some manually chosen corners and the transformation matrix was utilized for the registration.

Finally, a continuous genetic algorithm was developed for image fusion. The continuous GA has the advantage of less storage requirements than the binary GA and is inherently faster than the binary GA because the chromosomes do not have to be decoded prior to the evaluation of the cost function.

Data fusion provides an integrated image from a pair of registered and enhanced visual and thermal IR images. The fused image is invariant to illumination directions and is robust under low lighting conditions. They have potentials to significantly boost the performances of face recognition systems. One of the major obstacles in face recognition using visual images is the illumination variation. This challenge can be mitigated by using infrared (IR) images. On the other hand, using IR images alone for face recognition is usually not feasible because they do not carry enough detailed information. As a remedy, a hybrid system is presented that may benefit from both visual and IR images and improve face recognition under various lighting conditions.

# 7. References

+   - Bowyer W., Chang K. and Flynn P., A Survey of Approaches To Three-Dimensional Face Recognition, ICPR, Vol. 1, pp. 358 - 361, 2004.
+   - Dasarathy B. V., Image Fusion in the Context Of Aerospace Applications, Inform. Fusion, Vol. 3, 2002.
+   - Erkanli S. and Rahman Zia-Ur., Enhancement Technique for Uniformly and Non-Uniformly Illuminated Dark Images, ISDA 2010, Cairo, Egypt, 2010b.
+   - Erkanli S. and Rahman Zia-Ur., Wavelet Based Enhancement for Uniformly and Non-Uniformly Illuminated Dark Images, ISDA 2010, Cairo, Egypt, 2010c.
+   - Erkanli S.and Rahman Zia-Ur., Entropy Based Image Fusion With the help of Continuous Genetic Algorithm, IEEE ISDA Conference, December 2010.