# 12.4.2.5 Inherently Used Ontology

Without the notion of an ontology, some works on multi-label classification also exploit correlations among concepts.

Tsochantaridis et al. [95] proposed to generalize multi-class Support Vector Machine learning for interdependent and structured output spaces. Qi et al. [78] adopted a Gibbs Random Field to model the interaction between concepts, where the unary and pairwise potential function are learned simultaneously. Qi et al. [79] proposed to iteratively ask for the labels of the selected images to minimize the classification error rate under the active learning scenario.

There are clear advantages of leveraging ontology in traditional machine learning problems. This section provided details about the popularly applied ontologies as well as the very important ontological relations, such as Subclass and Co-occurrence. Many ontology-based algorithms are introduced and compared based on the relations they used. The result in their work showed the effectiveness and efficiency of ontology in diverse machine learning applications.

# 12.5 Geographical Classification with Multimedia Data

In recent years, there has been increasing geographically tagged multimedia on community Web sites such as Flickr,¹ and social networks (e.g., Facebook, Google+, Instagram), especially after the popularity of smart mobile devices. For instance, Flickr has reported over 100 million geotagged photos. Effectively organizing, searching, and discovering knowledge from such geotagged data are in great need. The research in geographical classification of multimedia is based on this.

Typically, geographical information has been studied in multimedia and computer vision research, within a contextual modeling framework. However, there are many possibilities for utilizing the geography as context, with different data modalities and purposes. The data types available for Geo-Information processing include GIS (Geographical Information System) databases, aerial or remote sensing images, unstructured geo-reference Web resources (e.g., images from blogs), and structured Web multimedia collections such as Flickr, Instagram et al., [58]. The purposes of these kinds of data may vary from geo-location annotation [32,45], retrieval [38], landmark recognition [18,104], to mining and recommendation (e.g., the tourism guide system) [35,37].

In this section, we focus on the problem of classification/recognition of structured Web multimedia that provides organized meta-data, especially for landmark recognition. The problem of geographical classification or landmark recognition aims at determining the location of an image, leveraging collections of geo-located images in the training set. The basic approach is to directly match feature points upon the indexing structure, or learn visual appearance models. It is an important research topic in various applications.

In the remainder of this section, we will first talk about the data and information available for Web multimedia, and then discuss the challenges in the geographical classification. Two detailed applications are explored, corresponding to the geo-classification of Web images, and of videos.

# 12.5.1 Data Modalities

The types of information available in structured Web multimedia for geographical classification include but ate not limited to the following:

+   1. GPS information: Mobile phones and smart devices, which record location information when taking photos. The GPS coordinates allow mapping images onto the globe, if the globe were