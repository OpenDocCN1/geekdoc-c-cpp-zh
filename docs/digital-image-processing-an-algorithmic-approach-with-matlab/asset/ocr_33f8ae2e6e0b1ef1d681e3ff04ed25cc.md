![](bbox=[0.13, 0.09, 0.85, 0.45])

# FIGURE 14.5 Face identification process.

Once the eigenfaces have been computed, the face space has to be populated with known faces. Usually, these faces are taken from the training set. Each known face is transformed into the face space, and its components stored in memory.

At this stage, the identification process can begin. An unknown face is presented to the system. The system projects it onto the face space and computes its distance from all the stored faces. The face is identified as being the same individual's as the face that is nearest to it in face space. There are several methods of computing the distance between multidimensional vectors. Here, a form of Mahalanobis distance is chosen. The identification process is summarized in Figure 14.5.

Figure 14.6 shows a test image with its eigenface components shown as images as well as 3D plots for better visualization.

An important fact should be noted. The identification process has been tested only on new images of individuals that made up the training set (out of the 10 mug shots of each individual, 2 were taken out of the training set to form the testing set). In fact, the identification of persons who were not included in the training set (but were in the populating set) is often very poor.