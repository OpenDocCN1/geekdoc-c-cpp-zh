
## 12.4.2.3 Co-Occurrence Relation

There is generally no unified ontological structure for the *Co-occurrence* relation. Therefore, the design of such algorithms is variable.

Li et al. [46] proposed a high-level image representation, called the “Object Bank,” where an image is represented as a scale-invariant response map of a large number of pre-trained generic object detectors, blind to the testing dataset or visual task. They leveraged a simple linear hypothesis classifier combined with a sparse-coding scheme to ensure both feature sparsity and object sparsity in the Object Bank representation, and also to grasp the semantic relations among these Objects (concepts).

Similarly, Smith et al. [86] proposed a two-step Discriminative Model Fusion (DMF) method for video annotation, which attempted to mine the relations among concepts by generating model vectors, based on detection of scores from individual detectors. The model vectors are then fed to a contextual Support Vector Machine (SVM) to refine the detection.

Tsai et al. [92] proposed a novel representation, called *Compositional Object Pattern*. This representation characterizes object-level patterns conveying much richer semantic information than low level visual features. Such an approach can help in more effective album classification, by interpreting the rich semantics in this kind of data. They first mined frequent object patterns in the training set, and then ranked them by their discriminating power. The album feature is then set to the frequencies of these discriminative patterns. Such frequencies are called *Compositional Object Pattern Frequency (COPF)* and classified by traditional classifiers such as SVM.

## 12.4.2.4 Combination of the Two Relations

In real applications, the *Subclass* relation and *Co-occurrence* relation usually co-exist in the ontology. Thus, much research has been done to leverage both relations simultaneously.

Marszalek et al. [59] proposed to use the semantics of image labels to integrate prior knowledge about the *Subclass* and *Co-occurrence* relationships into visual appearance learning. To create the semantic hierarchical classifier for object detection, they first queried WordNet with the class labels and extracted the knowledge in the form of a semantic hierarchy. This hierarchy is used for reasoning, and to organize and train the binary SVM detectors that are obtained by a state-of-the-art image classification method. Then, the trained hierarchical classifier can be used to efficiently recognize a large number of object categories.

Zha et al. [101] proposed a semantic ontology scheme for video annotation. They first leveraged LSCOM to construct the concept lexicon and described concept property as the weights of different modalities that were obtained manually or by a data-driven approach. They modeled *Subclass* and *Co-occurrence* relations separately. In particular, they propagated the initial detection of concepts to co-occurring concepts based on how likely they co-occur. On the other hand, the subclass relation is exploited by a hierarchical Bayesian network. Then these two refinements are concatenated to incorporate both relations.

Gao et al. [28] proposed to partition concepts into salient objects and scenes, in which the detection of salient objects utilizes object taxonomy, such as a subclass hierarchy, and to recognize scenes. A naive Bayesian framework modeling co-occurrence relation among salient object and scene is used. They claimed that their framework for hierarchical probabilistic image concept reasoning is scalable to diverse image contents with large within-category variations.

Tsai et al. [93] proposed a novel ontological visual inference framework that utilizes subclass and co-occurrence relations in the ontology to enhance multi-label image annotation. These two kinds of relations in the ontology are learned automatically: subclass relation is obtained via graph traversal techniques on WordNet’s hypernymy/hyponymy graph, and the statistical co-occurrence relation is learned from the training set. Their ontological inference framework then seeks the combination of labels that satisfies all the subclass constraints and scores the highest with co-occurrence reward or penalty.

## 12.4.2.5 Inherently Used Ontology

Without the notion of an ontology, some works on multi-label classification also exploit correlations among concepts.

Tsochantaridis et al. [95] proposed to generalize multi-class Support Vector Machine learning for interdependent and structured output spaces. Qi et al. [78] adopted a Gibbs Random Field to model the interaction between concepts, where the unary and pairwise potential function are learned simultaneously. Qi et al. [79] proposed to iteratively ask for the labels of the selected images to minimize the classification error rate under the active learning scenario.

There are clear advantages of leveraging ontology in traditional machine learning problems. This section provided details about the popularly applied ontologies as well as the very important ontological relations, such as Subclass and Co-occurrence. Many ontology-based algorithms are introduced and compared based on the relations they used. The result in their work showed the effectiveness and efficiency of ontology in diverse machine learning applications.

## 12.5 Geographical Classification with Multimedia Data

In recent years, there has been increasing geographically tagged multimedia on community Web sites such as Flickr,¹ and social networks (e.g., Facebook, Google+, Instagram), especially after the popularity of smart mobile devices. For instance, Flickr has reported over 100 million geotagged photos. Effectively organizing, searching, and discovering knowledge from such geotagged data are in great need. The research in geographical classification of multimedia is based on this.

Typically, geographical information has been studied in multimedia and computer vision research, within a contextual modeling framework. However, there are many possibilities for utilizing the geography as context, with different data modalities and purposes. The data types available for Geo-Information processing include GIS (Geographical Information System) databases, aerial or remote sensing images, unstructured geo-reference Web resources (e.g., images from blogs), and structured Web multimedia collections such as Flickr, Instagram et al., [58]. The purposes of these kinds of data may vary from geo-location annotation [32,45], retrieval [38], landmark recognition [18,104], to mining and recommendation (e.g., the tourism guide system) [35,37].

In this section, we focus on the problem of classification/recognition of structured Web multimedia that provides organized meta-data, especially for landmark recognition. The problem of geographical classification or landmark recognition aims at determining the location of an image, leveraging collections of geo-located images in the training set. The basic approach is to directly match feature points upon the indexing structure, or learn visual appearance models. It is an important research topic in various applications.

In the remainder of this section, we will first talk about the data and information available for Web multimedia, and then discuss the challenges in the geographical classification. Two detailed applications are explored, corresponding to the geo-classification of Web images, and of videos.

### 12.5.1 Data Modalities

The types of information available in structured Web multimedia for geographical classification include but are not limited to the following:

- 1. GPS information: Mobile phones and smart devices, which record location information when taking photos. The GPS coordinates allow mapping images onto the globe, if the globe were to be treated as a rectangular coordinate system, and the position is determined as latitude and longitude.

![](img/e042be977d84f1032c985f0d70b57c8b_382_0.png)

**FIGURE 12.8 (See color insert.):** The challenges in landmark image recognition. (a) and (b) are photos of Drum Tower of Xi’an and Qianmen Gate of Beijing, respectively. Though of different locations the visual appearances are similar due to historical and style reasons. (c) shows three disparate viewing angles of Lincoln Memorial in Washington, DC.

- 2. *Text information:* Typically, the textual meta-data such as the descriptions of Flickr images, or articles in personal blogs, contain named entities of positions (e.g., “Sydney Opera,” “Eiffel tower”). This is essential in indicating the geo-location of images. An example is [35], which extracted city names from MSN blogs and photo albums.
- 3. *Visual features:* Most problems deal with matching images to locations (e.g., landmark names). Visual features are of high importance for landmark recognition. Popular visual features include local points (e.g., SIFT [54]) and bag-of-words representations [84].
- 4. *Collaborative features:* With the popularity of social networks, collaborative features are also enhanced, especially for social media. Examples of collaborative features include *Hashing Tags* on Twitter labeled by users, and user comments or reposts. The problem of utilizing the collaborative features more efficiently still remains relatively unexplored, since some of them are highly unstructured and noisy.

Geographical classification always needs to fuse different modalities of information, to accurately predict geo-tags.

### 12.5.2 Challenges in Geographical Classification

The challenges of geographical classification of multimedia data are mainly due to the following two aspects:

- 1. *Visual ambiguity:* Different geo-locations may have similar visual appearance, because of historical or style reasons. More specifically, the building from the same period, or of the same style may not be distinguishable enough in terms of their visual features. This makes the construction of the visual appearance model for each landmark or class even more challenging.
- 2. *Geo-location ambiguity:* Even the same geo-location or landmark may look different from different visual angles. Though the advanced scale and rotation visual features such as SIFT [54] can handle the in-plane rotation, current image descriptors cannot address the out-of-plane rotation, i.e., the viewing angle changes.

Figure 12.8 shows two examples of these challenges. To deal with the visual ambiguity challenge, it is feasible to make use of multi-modality information, to eliminate these challenges. Classical approaches include fusing GPS position and visual features [37], or textual information and visual features [35].
