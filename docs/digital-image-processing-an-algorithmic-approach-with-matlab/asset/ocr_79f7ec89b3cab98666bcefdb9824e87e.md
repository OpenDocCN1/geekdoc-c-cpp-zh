```
title('Scatterplot of the segmented pixels in ' 'a*b*',
space');
xlabel('''a*'' values');
ylabel('''b*'' values');
```

# 12.8 SUMMARY

+   - Image classification and segmentation refers to finding and labeling areas in an image that bear some resemblance to each other.
+   - This can be used to isolate certain areas of interest from an image or segment them with similar colors to distinguish such areas within the image.
+   - Applications for such segmentation are found, in particular, in remote sensing and medical imaging and, in general, for any image processing system. For instance, the classification technique can be used to categorize roads from fields in a satellite image.
+   - The basis of classification is to find areas of similar characteristics and mark them.
+   - These characteristics are called the features or attributes of each class, and can be calculated in a variety of ways. In this chapter, only color gray-scale-based features are presented.
+   - If the features are calculated based on some guideline applied to the source image in order to identify a class through this guideline, then such a classification technique is called supervised classification.
+   - If, on the other hand, the classification is done automatically based on some form of clustering, then it is called unsupervised classification.
+   - Unsupervised classification is usually more time consuming than the supervised method.
+   - A variety of techniques have been reported in the literature to perform these classifications, and they vary in their accuracy and speed of application.