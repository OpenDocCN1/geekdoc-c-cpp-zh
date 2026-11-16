Otsu's method [8.38] is very effective in analyzing histograms of bimodal images. It automatically calculates the optimal threshold that minimizes the within-class variance (or equivalently, maximizes the between-class variance. Students will have the opportunity to prove this statement in Assignment 8.2). The procedure of Otsu's method is described below:

+   **Otsu's Method**
+   
+   1. Compute the histogram and the probability, _P_(_i_), of the input image, where _i_ is the index of possible intensity levels in the input image, e.g., _i_ = 0, ..., _L_.
+   
+   2. For each possible threshold value, _t_, _t_ \(\in\) [0, _L_], calculate the within-class variance, \(\sigma_w^2(t)\),
+   
+      \(\sigma_w^2(t) = w_1(t)\sigma_1^2(t) + w_2(t)\sigma_2^2(t)\) (8.1)
+   
+      where \(w_1(t) = \sum_{i=0}^{t-1} P(i)\) and \(w_2(t) = \sum_{i=t}^{L} P(i)\) are the weights that estimate the class probabilities, and the variance of each class is calculated as
+   
+      \(\sigma_1^2(t) = \sum_{i=0}^{t-1} [i - \mu_1(t)]^2 P(i)/w_1(t), \sigma_2^2(t) = \sum_{i=t}^{L} [i - \mu_2(t)]^2 P(i)/w_2(t),\) (8.2)
+   
+      where \(\mu_1(t) = \sum_{i=0}^{t-1} iP(i)/w_1(t)\) and \(\mu_2(t) = \sum_{i=t}^{L} iP(i)/w_2(t)\) are the means of each class.
+   
+   3. The optimal threshold is the one that minimizes \(\sigma_w^2(t)\).

Given the equivalence mentioned above, this procedure can also be revised to maximize the between-class variance,

\(\sigma_b^2(t) = w_1(t)w_2(t)[\mu_1(t) - \mu_2(t)]^2.\) (8.3)

The benefit of having a maximization formulation is that it allows the between-class variance to be calculated in a recursive manner, speeding up the exhaustive search procedure of Otsu's method, which is otherwise quite time consuming. The proof of Eq. 8.3 as well as its recursive calculation nature is a homework problem (Assignment 8.3). Figure 8.6 shows two synthetic images, their histograms, and the thresholding results using Otsu's method. We can see that when the histogram is bimodal, Otsu's method works very effectively even with 20dB Gaussian noise added to the image. However, if the histogram is not bimodal, e.g., exhibiting three peaks, Otsu's method fails to generate a reasonable segmentation result.

In the following sections, two more sophisticated techniques for finding the optimal threshold are described.

# 8.2.3 Fitting the Histogram with a Sum of Gaussians

Given a bimodal histogram, _h_(_f_), of an image, where _f_ represents a brightness value, a standard technique [8.17] to find the best threshold of that image is to fit the histogram