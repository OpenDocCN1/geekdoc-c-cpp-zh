Section 4 presents the proposed image fusion algorithm. Section 5 reports the experimental results of the proposed algorithm. Section 6 concludes this research.

# 2. Literature survey

In this section, we will present related work in IR Image technology, nonlinear image enhancement algorithms, image registration and image fusion.

# 2.1 IR tecnology

One type of electromagnetic radiation that has received a lot of attention recently is Infrared (IR) radiation. IR refers to the region beyond the red end of the visible color spectrum, a region located between the visible and the microwave regions of the electromagnetic spectrum.

Today, infrared technology has many exciting and useful applications. In the field of infrared astronomy, new and fascinating discoveries are being made about the Universe and medical imaging as a diagnostic tool.

Humans, at normal body temperature, radiate most strongly in the infrared, at a wavelength of about 10 microns. The area of the skin that is directly above a blood vessel is, on average, 0.1 degrees Celsius warmer than the adjacent skin. Moreover, the temperature variation for a typical human face is in the range of about 8 degrees Celsius [F. Prokoski, 2000].

In fact, variations among images from the same face due to changes in illumination, viewing direction, facial expressions, and pose are typically larger than variations introduced when different faces are considered. Thermal IR imagery is invariant to variations introduced by illumination facial expressions since it captures the anatomical information. However, thermal imaging has limitations in identifying a person wearing glasses because glass is a material of low emissivity, or when the thermal characteristics of a face have changed due to increased body temperature (e.g., physical exercise) [G. S. Kong et al., 2005]. Combining the IR and visual techniques will benefit face detection and recognition.

# 2.2 Nonlinear image enhancement techniques

# 2.2.1 The nonlinear log transform

The non-linear log transform converts an original image g into an adjusted image g' by applying the log function to each pixel g[m, n] in the image, $g'[m, n] = k log(g[m, n])$ (1) where $k = L/log(L)$ is a scaling factor that preserve the dynamic range and L is intensity. The log transformis typically applied either to dark images where the overall contrast is low, or to images that contain specular reflections or glints. In the former case, the brightening of the dark pixels leads to an overall increase in brightness. In the latter case, the glints are suppressed thus increasing the effective dynamic range of the image.

The log function as defined in equation 1 is not parameterized, i.e. it is a single input/output transfer function. A modified parameterized function was proposed by Schreiber in [W. F. Schreiber, 1978] as: image,