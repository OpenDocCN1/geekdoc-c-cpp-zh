
Section 4 presents the proposed image fusion algorithm. Section 5 reports the experimental results of the proposed algorithm. Section 6 concludes this research.

## 2. Literature survey

In this section, we will present related work in IR image technology, nonlinear image enhancement algorithms, image registration and image fusion.

### 2.1 IR technology

One type of electromagnetic radiation that has received a lot of attention recently is Infrared (IR) radiation. IR refers to the region beyond the red end of the visible color spectrum, a region located between the visible and the microwave regions of the electromagnetic spectrum.

Today, infrared technology has many exciting and useful applications. In the field of infrared astronomy, new and fascinating discoveries are being made about the Universe and medical imaging as a diagnostic tool.

Humans, at normal body temperature, radiate most strongly in the infrared, at a wavelength of about 10 microns. The area of the skin that is directly above a blood vessel is, on average, 0.1 degrees Celsius warmer than the adjacent skin. Moreover, the temperature variation for a typical human face is in the range of about 8 degrees Celsius [F. Prokoski, 2000].

In fact, variations among images from the same face due to changes in illumination, viewing direction, facial expressions, and pose are typically larger than variations introduced when different faces are considered. Thermal IR imagery is invariant to variations introduced by illumination and facial expressions since it captures the anatomical information. However, thermal imaging has limitations in identifying a person wearing glasses because glass is a material of low emissivity, or when the thermal characteristics of a face have changed due to increased body temperature (e.g., physical exercise) [G. S. Kong et al., 2005]. Combining the IR and visual techniques will benefit face detection and recognition.

### 2.2 Nonlinear image enhancement techniques

#### 2.2.1 The nonlinear log transform

The non-linear log transform converts an original image \(g\) into an adjusted image \(g'\) by applying the log function to each pixel \(g[m,n]\) in the image,

\[
g'[m,n] = k \log(g[m,n]) \tag{1}
\]

where \(k = L/\log(L)\) is a scaling factor that preserves the dynamic range and \(L\) is intensity. The log transform is typically applied either to dark images where the overall contrast is low, or to images that contain specular reflections or glints. In the former case, the brightening of the dark pixels leads to an overall increase in brightness. In the latter case, the glints are suppressed thus increasing the effective dynamic range of the image.

The log function as defined in equation 1 is not parameterized, i.e. it is a single input/output transfer function. A modified parameterized function was proposed by Schreiber in [W. F. Schreiber, 1978] as:

\[
g'(l) = (L-1)\left[\frac{\log(1+\alpha g(l))-\log(\alpha+1)}{\log(1+\alpha L)-\log(\alpha+1)}\right]+1 \tag{2}
\]

where \(\alpha\) parameterizes the non-linear transfer function.

### 2.3 Registration

Image registration is a basic task in image processing to align two or more images, usually referred to as a reference, and a sensed image [R. C. Gonzalez et al., 2004]. Registration is typically a required process in remote sensing [L. M. G. Fonseca & B. S. Manjunath, 1996], medicine and computer vision. Registration can be classified into four main categories according to the manner how the image is obtained [B. Zitova & J. Flusser, 2003]:

- Different viewpoints: Images of the same scene taken from different viewpoints.
- Different times: Images of the same scene taken at different times.
- Different sensors: Images of the same scene taken by different sensors.
- Scene-to-model registration: Images of a scene taken by sensors and images of the same scene but from a model (digital elevation model).

It is impossible to implement a comprehensive method usable for all registration tasks, and there are many different registration algorithms. The focus is on the feature-based registration techniques in this research and they usually consist of the following three steps [B. Zitova & J. Flusser, 2003].

- Feature detection: The step tries to locate a set of control points such as edges, line intersections and corners in the image. They could be manually or automatically detected.
- Feature matching: The second step is to establish the correspondence between the features detected in the sensed image and those detected in the reference image.
- Transform model estimation, image resampling and geometric transformation: The sensed image is transformed and resampled to match the reference image by proper interpolation techniques [B. Zitova & J. Flusser, 2003].

Each registration step has its specific problems. In the first step, features that can be used for registration must spread over the images and be easily detectable. The determined feature sets in the reference and sensed images must have enough common elements, even though both images do not cover exactly the same scene. Ideally, the algorithm should be able to detect the same features [B. Zitova & J. Flusser, 2003].

In the second step, known as feature matching, physically corresponding features can be dissimilar because of the different imaging conditions and/or the different spectral sensitivities of the sensors. The choice of the feature description and measuring of similarity has to take these factors into account. The feature descriptors should be efficient and invariant to the assumed degradations. The matching algorithm should be robust and efficient. Single features without corresponding counterparts in the other image should not affect its performance [B. Zitova & J. Flusser, 2003].

In the last step, the selection of an appropriate resampling technique is restricted by the trade-off between the interpolation accuracy and the computational complexity. In the literature, there are popular techniques such as the nearest-neighbor and bilinear interpolation [B. Zitova & J. Flusser, 2003].

### 2.4 Genetic Algorithm

#### 2.4.1 Introduction

Optimization can be distinguished by either discrete or continuous variables. Discrete variables have only a finite number of possible values, whereas continuous variables have an infinite number of possible ones. Discrete variable optimization is also known as combinatorial optimization, because the optimum solution consists of a certain combination of variables from the finite pool of all possible variables. However, when trying to find the minimum value of \(f(x)\) on a number line, it is more appropriate to view the problem as continuous [J. H. Holland, 1975; S. K. Mitra et al., 1998].

Genetic algorithms manipulate a population of potential solutions for the problem to be solved. Usually, each solution is coded as a binary string, equivalent to the genetic material of individuals in nature. Each solution is associated with a fitness value that reflects how good it is, compared with other solutions in the population. The higher the fitness value of an individual, the higher its chances of survival and reproduction in the subsequent generation. Recombination of genetic material in genetic algorithms is simulated through a crossover mechanism that exchanges portions between strings.

Another operation, called mutation, causes sporadic and random alteration of the bits in strings. Mutation has a direct analogy in nature and plays the role of regenerating lost genetic material [M. Srinivas & L. M. Patnaik, 1994]. GAs have found applications in many fields including image processing [J. Zhang, 2008; L. Yu et al., 2008].

#### 2.4.2 Continuous Genetic Algorithm (CGA)

GAs typically represent solutions as binary strings. For many applications, it is more convenient to denote solutions as real numbers known as continuous genetic algorithms (CGA). CGAs have the advantage of requiring less storage and are faster than the binary counterparts. Figure 1 shows the flowchart of a simple CGA [Randy L. Haupt & Sue Ellen Haupt, 2004].

##### 2.4.2.1 Components of a Continuous Genetic Algorithm

The various elements in the flowchart are described below [D. Patnaik, 2006].

###### 2.4.2.1.1 Cost function

The goal of GAs is to solve an optimization problem defined as a cost function with a set of parameters involved. In CGA, the parameters are organized as a vector known as a chromosome. If the chromosome has \(N_{\mathrm{var}}\) variables (an \(N\)-dimensional optimization problem) given by \(p_1, p_2, p_3, \ldots, p_{N_{\mathrm{var}}}\), then the chromosome is written as an array with \(1 \times N_{\mathrm{var}}\) elements as [Randy L. Haupt & Sue Ellen Haupt, 2004]:

\[
\text{chromosome} = [p_1, p_2, p_3, \ldots, p_{N_{\mathrm{var}}}] \tag{3}
\]
