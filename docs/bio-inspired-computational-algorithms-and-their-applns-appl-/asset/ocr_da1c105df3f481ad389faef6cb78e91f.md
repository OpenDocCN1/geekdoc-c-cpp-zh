# 6.2.2 Genetic algorithm set up

# 6.2.2.1 Coding the chromosome

The chromosome is comprised of the parameters of the filter bank described in equation 43.
The number of sub-bands is fixed, and each one of the centers and bandwidths are subject to the genetic algorithm. Real numbers are used.

# 6.2.2.2 The cost function

The cost function is given by equation (32), criterion J₂. The goal is to maximize J₂ as a function of the centers and bandwidths.

# 6.2.2.3 Restrictions

The following restrictions apply:

R1. Sub-bands overlapping <= 50Hz,
R2. Bandwidth is limited to range from 40 to 400 Hz, varying according to the performance of the genetic algorithm.

# 6.2.2.4 Operating parameters of the genetic algorithm

The main parameters of the genetic algorithm are summarized in the Table 1. The values of the parameters are given according to the best results obtained by experimentation. The genetic algorithm was ran in Matlab®, using the genetic algorithms toolbox and the gatool guide. The nomenclature of the parameters in Table 1 is the one used by Matlab®.

# 6.2.2.5 Application’s algorithm

To make operational de methodology described so far, the following steps apply:

+   1. **Vocabulary definition.** 2 to K words. In many real life applications, K in 8 to 15 words do the job.
+   2. **Database acquisition.** 15 to 20 utterances of each word from the vocabulary, for learning purposes. The sampling frequency can be set from 6000 to 8000 Hz. Human voice accommodates easily here.
+   3. **s(t) to S(w) transformation.** Apply Fourier transform to the data, normalize to unitary amplitude and to a fixed length of 2000.
+   4. **Data preparation for the GA.** Set-up the size (eq. 43) and restrictions (subsection 6.2.2.3) of the filter bank (chromosome).
+   5. **Running the GA.** Run the GA to find the sub-bands whose J₂ (eq. (32)) is the maximum.
+   6. **Filters realization.** For each sub-band, compute the coefficients of the respective bandpass filters. For real-time implementation, order from 4 to 8 is recommended, type IIR, elliptic. Elliptic filters achieve great discrimination and selectivity. Implementation details can be found in [2].
+   7. **Modeling the commands.** To make comparisons and therefore classification, a Gaussian statistical model of each word is to be constructed for each command in the vocabulary. Proceed as follows for each command:
+      a. Construct a matrix C of 15-20 rows of S_r_n(w) and M columns (one row per sample of the command, one column per sub-band selected by the AG),
+      b. Compute the mean value overall the samples, to find the average energy per sub-band, this is the feature vector of the command (μ)