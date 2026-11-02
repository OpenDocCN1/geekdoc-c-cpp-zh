
## 6. Conclusions

In this chapter, a database for visual and thermal images was created and several techniques were developed to improve image quality as an effort to address the illumination challenge in face recognition.

Firstly, one image enhancement algorithm was designed to improve the images' visual quality. Experimental results showed that the enhancement algorithm performed well and provided good results in terms of both luminance and contrast enhancement. In the luminance enhancement part, it has been shown that the proposed algorithm worked well for both dark and bright images. In the contrast enhancement part, it was proven that the proposed nonlinear transfer functions could make unseen or barely seen features in low contrast images clearly visible.

Secondly, the IR and enhanced visual images taken from different sensors, viewpoints, times and resolution were registered. A correspondence between an IR and a visual image was established based on a set of image features detected by the Harris Corner detection algorithm in both images. A spatial transformation matrix was determined based on some manually chosen corners and the transformation matrix was utilized for the registration.

Finally, a continuous genetic algorithm was developed for image fusion. The continuous GA has the advantage of less storage requirements than the binary GA and is inherently faster than the binary GA because the chromosomes do not have to be decoded prior to the evaluation of the cost function.

Data fusion provides an integrated image from a pair of registered and enhanced visual and thermal IR images. The fused image is invariant to illumination directions and is robust under low lighting conditions. They have potentials to significantly boost the performances of face recognition systems. One of the major obstacles in face recognition using visual images is the illumination variation. This challenge can be mitigated by using infrared (IR) images. On the other hand, using IR images alone for face recognition is usually not feasible because they do not carry enough detailed information. As a remedy, a hybrid system is presented that may benefit from both visual and IR images and improve face recognition under various lighting conditions.

## 7. References

- Bowyer W., Chang K. and Flynn P., A Survey of Approaches To Three-Dimensional Face Recognition, ICPR, Vol. 1, pp. 358-361, 2004.
- Dasarathy B. V., Image Fusion in the Context Of Aerospace Applications, Inform. Fusion, Vol. 3, 2002.
- Erkanli S. and Rahman Zia-Ur., Enhancement Technique for Uniformly and Non-Uniformly Illuminated Dark Images, ISDA 2010, Cairo, Egypt, 2010b.
- Erkanli S. and Rahman Zia-Ur., Wavelet Based Enhancement for Uniformly and Non-Uniformly Illuminated Dark Images, ISDA 2010, Cairo, Egypt, 2010c.
- Erkanli S. and Rahman Zia-Ur., Entropy Based Image Fusion With the help of Continuous Genetic Algorithm, IEEE ISDA Conference, December 2010.
- Fonseca L. M. G. and Manjunath B. S., Registration Techniques for Multisensor Remotely Sensed Imagery, Photogrammetric Engineering & Remote Sensing, Vol. 62, pp. 1049-1056, 1996.
- Gonzalez R. C., Woods R. E. and Eddins S. L., Digital Image Processing, Pearson Education, Inc. Prentice Hall, 2004.
- Haupt Randy L. and Haupt Sue Ellen, Practical Genetic Algorithms, Second Edition, ISBN 0-471-45565-2 Copyright © 2004 John Wiley & Sons, Inc.
- Hines G. D., Rahman Z., Jobson D. J., and Woodell G. A., Single-Scale Retinex Using Digital Signal Processors In Proceedings Of The GSPX, 2004.
- Holland J. H., Adaptation In Natural and Artificial Systems, University of Michigan Press, 1975.
- Hurlbert A. C., The Computation of Color, Ph.D. Dissertation, Mass. Inst. Tech., Cambridge, MA, Sept. 1989.
- Jobson D. J., Rahman Z. and Woodell G. A., Properties and Performance of a Center/Surround Retinex, IEEE Trans. Image Processing, Vol. 6, pp. 451-462, 1997.
- Kannan K. and Perumal S., Optimal Decomposition Level of Discrete Wavelet Transform for Pixel Based Fusion of Multi-Focused Images, International Conference On Computational Intelligence And Multimedia Applications, 2007.
- Kolb H., How the Retina Works, American Scientist, Vol. 91, 2003.
- Kong G. S., Heo J., Abidi B. R., Paik J. and Abidi M. A., Recent Advances in Visual and Infrared Face recognition – a Review, Computer Vision and Image Understanding, Vol. 1, pp. 103-135, 2005.
- Land E., An Alternative Technique For The Computation Of The Designator In The Retinex Theory of Color Vision, Proc. of the National Academy of Sciences USA, Vol. 83, pp. 3078-3080, 1986.
- Mahani S., Ho J., Vetter T. and Kriegman D. J., Face Recognition Using 3-D Models: Pose and Illumination, Proceedings of the IEEE, Vol. 94, pp. 1977-1999, 2006.
- Mitra S. K., Murthy C. A. and Kundu M. K., Technique for Fractal Image Compression using Genetic Algorithm, IEEE Trans. Image Process., pp. 586-593, 1998.
- Mumtaz A. and Majid A., Genetic Algorithms and its application to Image Fusion, International Conference On Emerging Technologies ICET, 2008.
- Patnaik D., Biomedical Image Fusion using Wavelet Transforms and Neural Network, IEEE International Conference on Industrial Technology, pp. 1189-1194, 2006.
- Pattichis C. S. and Pattichis M. S., Medical Imaging Fusion Applications — An Overview, In Conf. Rec. Asilomar Conf. Signals, Systems, Computers, Vol. 2, pp. 1263-1267, 2001.
- Prokoski F., History, Current Status, and Future of Infrared Identification, Computer Vision Beyond the Visible Spectrum: Methods and Applications, Proceedings IEEE Workshop, pp. 5-14, 2000.
- Rahman Z., Jobson D. and Woodell G. A., Multiscale Retinex For Color Image Enhancement, In Proceedings of the IEEE International Conference On Image Processing, 1996.
- Rahman Z., The Lecture Notes of Image Processing, Old Dominion University, 2009.
- Rahman Z., Woodell G. A. and Jobson D., A Comparison of The Multiscale Retinex with other Image Enhancement Techniques, In Proceedings Of The IS&T 50th Anniversary Conference, pp. 426-431, 1997b.
- Schreiber W. F., Image processing for quality improvement, Proceedings of the IEEE, Vol. 66, pp. 1640-1651, 1978.
- Socolinsky D. A. and Selinger A., A Comparative Analysis of Face Recognition Performance with Visible and Thermal Infrared Imagery, IEEE International Conference of Pattern Recognition, Vol. 4, pp. 217-222, 2002.
- Srinivas M. and Patnaik L. M., Genetic Algorithms: a Survey, pp. 17-26, Vol. 27, Jun 1994.
- Tao L., An Adaptive And Integrated Neighborhood Dependent Approach For Nonlinear Enhancement Of Color Images, SPIE Journal of Electronic Imaging, pp. 1-14, 2005.
- Tao L., Tompkins R. C., and Asari K. V., An Illuminance Reflectance Model For Nonlinear Enhancement Of Video Stream For Homeland Security Applications, IEEE International Workshop on Applied Imagery and Pattern Recognition, AIPR, October 19-21, 2005.
- Wang A., Sun H. and Guan Y., The Application of Wavelet Transform to Multi-Modality Medical Image Fusion, Networking, Sensing and Control, ICNSC Proceedings Of The 2006 IEEE International Conference, pp. 270-274, 2006.
- Wang H., Multisensor Image Fusion by using Discrete Multiwavelet Transform, The Third International Conference on Machine Learning and Cybernetics, Shanghai, 26-29 August 2004.
- Wilson T. A., and Rogers S. K., Perceptual-Based Image Fusion for Hyperspectral Data, IEEE Trans. Geoscience and Remote Sensing, Vol. 35, pp. 1007-1017, July 1997.
- Yu L., Yung T., Chan K., Ho Y. and Ping Chu Y., Image Hiding with an improved Genetic Algorithm and an Optimal Pixel Adjustment Process, Eighth International Conference On Intelligent Systems Design And Applications, 2008.
- Zhang J., Feng X., Song B., Li M. and Lu Y., Multi-Focus Image Fusion using Quality Assessment of Spatial Domain And Genetic Algorithm, Human System Interactions, pp. 71-75, 25-27 May 2008.
- Zitova B. and Flusser J., Image Registration Methods: A Survey, Image and Vision Computing 21, pp. 977-1000, 2003.

## Self Adaptive Genetic Algorithms for Automated Linear Modelling of Time Series

Pedro Flores<sup>1</sup>, Larysa Burtseva<sup>2</sup> and Luis B. Morales<sup>3</sup>

<sup>1</sup>Universidad de Sonora  
<sup>2</sup>Universidad Autónoma de Baja California  
<sup>3</sup>Universidad Nacional Autónoma de México  
Mexico

### 1. Introduction

In this work it is developed a methodological proposal to build linear models of Time Series (TS) from setting out the problem of obtaining a good linear model, such as solving a problem of nonlinear optimization with bounded variables. It is worth to mention that to build these problems are taken some ideas of the traditional statistical approach.

As product of the methodology here presented, it will be developed two heuristic algorithms for the treatment of TS, which allow building several models for the same problem, where the accuracy of these can be increased by increasing the number of terms of the model, situation that does not happen with the traditional statistical approach. Thus, with this algorithms it can be obtained several proposals of solution for the same problem, of which it can be selected the one that presents the best results in the forecasting. In addition, the algorithms proposed in this work allow building different linear versions, but equivalent to the Autoregressive (AR) and the classic Autoregressive with Moving Average (ARMA) models, with the added advantage of the possibility of obtaining models for not stationary TS, and with non stationary variance, in cases where the traditional methodology does not work.

Since optimization problems set out here may present multiple local minimums, it is needed to use a special technique to solve them. With this end it was developed a version of the Self Adaptive Genetic Algorithms (SAGA), encoded on real numbers that allows, without intervention of the user, to find satisfactory solutions for different problems without making changes in the parameters of the code.

On the other hand, among the principal points of this methodology it is the fact that in many cases, these linear versions present a phenomenon that has been named 'forecasting delay', which allows to modify the linear model obtained to find a more accurate forecasting.

It is important to notice that the first AR version of the algorithms developed for the TS were tested in the examples of the international competition:

> **"NN3 Artificial Neural Networks & Computational Intelligence Forecasting Competition"**

that from now on it will be called NN3, which was realized in 2006-2007 (http://www.neural-forecasting-competition.com/NN3/results.htm). This competition is
