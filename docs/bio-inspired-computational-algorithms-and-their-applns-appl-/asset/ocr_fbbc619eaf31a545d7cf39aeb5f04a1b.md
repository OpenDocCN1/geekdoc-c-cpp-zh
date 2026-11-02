calibrated in field conditions because of constraints on time. Figure 3 shows an example where the IR and visual image were captured at the same time. It is obvious from the figure that the images need to be registered before they can be fused since the field-of-view and the pixel resolution are obviously different.

The performance of the proposed algorithm was tested and compared with different PLIF methods. The IR and visual images were not previously registered as shown in Figure 3. The registered image, base image (IR Image) and fused image with CGA are shown in Figure 4. The cost function is very simple and defined as:

Entropy(F = w_V V + w_IR IR) (38)

where V and IR are the visual and IR images, w_V and w_IR are the respective associated weights, and F is the fused image. The initial population size is 100x3. The first and second columns in population matrix represent w_V and w_IR and the last column represents the cost function which is the entropy of F. Then initial population has been ranked based on the cost. In each iteration of the GA, 20 of the 100 rows are kept for mating and the rest are discarded. The crossover has been applied based on the Equation 35. The mutation rate was set to 0.20, hence the total number of mutated variables is 40. The value of a mutated variable is replaced by a new random value in the same range.

![](bbox=[0.25, 0.62, 0.75, 0.75])

Fig. 3. Visual and IR Images: Left: Visual Image, Right: IR Image.

# Registered Image

# IR Image

# Fused Image

![](bbox=[0.15, 0.86, 0.9, 0.94])

Fig. 4. The Result of Fusion: Left: Registered Images, Middle: IR Image Right: Fused Image with GA

The CGA results after 50 iterations of the GA such that the CGA maximize the cost and find optimum weights of images. In the 2nd, 8th, and 25th iterations, the cost increased but was not associated with the global solution. The optimum solution was determined in 45th iteration and remained unchanged because it is optimum solution. Figure 4 shows the fusion results of point-rules based PLIF. After registering IR and visual data, we determined that w_V = 0.9931 and w_IR = 0.0940 provide the optimum values for maximizing the entropy cost function for the F specified in Equation 38. The evaluation of these weights results is shown in Table 2. Table 2 shows that CGA based fusion method gives better results