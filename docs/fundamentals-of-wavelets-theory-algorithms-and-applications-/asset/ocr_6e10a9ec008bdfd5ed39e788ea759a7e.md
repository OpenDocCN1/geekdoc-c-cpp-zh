The American Association of Railroads (AAR) provides us with acoustic signals of 18 different types of bearing faults in two classes of sizes, the E-class and the F-class. Each data set is about 0.5 megabytes sampling at greater than 260 KHz. Each bearing was tested under two different load conditions, and the wheel was rotating at equivalent train speeds of 30-80 mph. Only 25 percent of each data set was used for training the feature vector in every case. The recognition algorithm is given in Figure 9.13.

# FIGURE 9.13: A block diagram of faulty bearing detection algorithm.

![](bbox=[0.14, 0.39, 0.85, 0.75])

# 9.5.2 Wavelets, Wavelet Packets, and FFT Features

The number of samples in each training data is 2^12. The formation of the feature vectors for each technique is given as follows: