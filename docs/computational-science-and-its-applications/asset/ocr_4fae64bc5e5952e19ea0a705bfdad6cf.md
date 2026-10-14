![](bbox=[0.16, 0.11, 0.84, 0.46])

# FIGURE 12.5

Matching score of phase symmetry features.

not offer the inference that two templates in the database belong to the same person, rather it is an indicator of the difficulty of recognition in comparing the two templates [63]. The similarity measure of the right and left palm can be seen using the Matching Score button on Panel 5.

# 12.4 Results and Discussion

To evaluate the performance of the GUI proposed for palmprint recognition, the following parameters have been calculated.

# 12.4.1 Texture Features

Feature extraction is a process of extracting the information from the image such that distinctive properties of extracted features help in differentiating between the categories of input patterns. Feature extraction is also preferred to reduce the cost of feature measurements, to increase classifier efficiency, and allows higher matching accuracy to identify an individual. The image of the palm is rich in texture features like ridges, valleys, principal lines, color etc. Thus, the use of a proper texture description scheme is expected to capture this information accurately. To extract the principal lines as texture feature of the palmprint, function segment_palm(im) is used to segment the image into separate palms i.e., right palm and left palm and function palm_features(left_image,