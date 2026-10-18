
## 12.1 Introduction

Many machine classification problems resemble human decision making tasks, which are multi-modal in nature. Humans have the capability to combine various types of sensory data and associate them with natural language entities. Complex decision tasks such as person identification often heavily depend on such synergy or fusion of different modalities. For that reason, much effort on machine classification methods goes into exploiting the underlying relationships among modalities and constructing an effective fusion algorithm. This is a fundamental step in the advancement of artificial intelligence, because the scope of learning algorithms is not limited to one type of sensory data.

This chapter is about multimedia classification, a decision making task involving several types of data such as audio, image, video (time sequence of images), and text. Although other modalities, e.g., haptic data, may fall into the category of multimedia, we only discuss audio, visual, and text because they represent a broad spectrum of both human decision tasks and machine learning applications.

### 12.1.1 Overview

Advances in modern digital media technologies has made generating and storing large amounts of multimedia data more feasible than ever before. The World Wide Web has become a huge, diverse, dynamic, and interactive medium for obtaining knowledge and sharing information. It is a rich and gigantic repository of multimedia data collecting a tremendous number of images, music, videos etc. The emerging need to understand large, complex, and information-rich multimedia content on the Web is crucial to many data-intensive applications in the field of business, science, medical analysis, and engineering.

The Web (or a multimedia database in general) stores a large amount of data whose modality is divided into multiple categories including audio, video, image, graphics, speech, text, document, and hypertext, which contains text markups and linkages. Machine classification on the Web is an entire process of extracting and discovering knowledge from multimedia documents on a computer-based methodology. Figure 12.1 illustrates the general procedure for multimedia data learning.

Multimedia classification and predictive modeling are the most fundamental problems that resemble human decision making tasks. Unlike learning algorithms that focus within a single domain,

![](img/e042be977d84f1032c985f0d70b57c8b_367_0.png)

# FIGURE 12.1 (See color insert.): Flowchart of general multimedia learning process.

many questions are open in information fusion. Multimedia classification studies how to fuse dependent sources, modalities, or samples efficiently to achieve a lower classification error. Most of the learning algorithms can be applied to multimedia domain in a straightforward manner. However, the specificity of an individual model of data is still very significant in most real-world applications and multimedia system designs. To shed more light on the problems of multimedia classification, we will first introduce the three fundamental types of data including audio, visual, and text.

Audio and visual are essential sensory channels for humans to acquire information about the world. In multimedia classification, the fusion of audio and visual has been extensively studied, and achieved different levels of improvement in tasks including event detection, person identification, and speech recognition, when compared to methods based on only one modality. In this chapter we survey several important related topics and various existing audio-visual fusion methods.

Text is quite different from any sensory modality. It is in the form of natural language, a special medium for human to exchange knowledge. There is an unproven hypothesis in neuroscience that the human brain associates patterns observed in different sensory data to entities that are tied to basic units in natural language [43]. This hypothesis coincides with the recent efforts on ontology, a graphical knowledge representation that consists of abstract entities with semantically meaningful links, and learning algorithms to build the connection among natural language, ontology, and sensory data (mostly images).

In this chapter, we mainly focus on decision making from multi-modality of data in an application-oriented manner instead of illustrating different learning algorithms. The remainder of this chapter is organized as follows. In Section 12.2, we illustrate commonly used features for the three fundamental data types. Audio-visual fusion methods and potential applications are introduced in Section 12.3. Section 12.4 explains how to use ontological structure to enhance multimedia machine classification accuracy. We then discuss geographical classification using multimedia data in Section 12.5. Finally, we conclude this chapter and discuss future research directions in the field of Multimedia.

## 12.2 Feature Extraction and Data Pre-Processing

Existing learning algorithms in a variety of fields frequently rely on vectorized data, because each sample input can be easily expressed mathematically as an individual point abstracted in some

Euclidean space. Although in the modern digital world, data can be naturally represented as vectors, finding discriminative features in a meaningful feature space is extremely important. We call the process of studying meaningful data representation and discovering knowledge from the data as feature extraction.

![](img/e042be977d84f1032c985f0d70b57c8b_368_0.png)

FIGURE 12.2 (See color insert.): Time-domain waveform of the same speech from different persons [80].

![](img/e042be977d84f1032c985f0d70b57c8b_368_1.png)

FIGURE 12.3 (See color insert.): Frequency response of the same speech in Figure 12.2 [80].

In general, good features can make the learning problem trivial. Conversely, bad representations will make the problem unsolvable in the extreme case. A simple example in the context of speech recognition is illustrated in Figure 12.2. Both waveforms are exactly the same sentence spoken by different people. One can easily observe large deviations between the two, which make it difficult to visually determine whether the two signals indicate the same speech without the explicit help of professionals in the field. However, if we transfer them into the frequency domain using a short time Fourier Transform, the harmonics shown in Figure 12.3 on different frequencies over time are almost identical to each other. This simple example suggests that raw signal data is rarely used as input for machine classification algorithms. We now briefly introduce some common features that have been widely used in the multimedia community. This simple example demonstrates how raw signal data is quite limited in its ability to model the content that is relevant for machine classification algorithms.

### 12.2.1 Text Features

Text data preprocessing and feature extraction are very important for text categorization, a conventional classification task that assigns pre-defined categories to text content. However, unlike

images and audios, text documents do not have a natural feature representation. To alleviate the problem, the most popular and the simplest feature is a bag-of-words, which vectorizes the text documents. Bag-of-words feature extraction uses the relative frequency of occurrences of a set of keywords as a quantitative measure to convert each text document to a vector. The reason for using relative frequencies instead of absolute word counts is to reduce the effect of length difference among documents.

Furthermore, feature extraction usually involves some data preprocessing steps such as data cleaning and normalization. By removing unwanted details and “normalizing” data, learning performances can be significantly improved. For instance, in text documents, punctuation symbols and non-alphanumeric characters are usually filtered because they do not contribute to feature discrimination. Moreover, words that occur too frequently such as “the,” “a,” “is,” and “at” are also discarded because of their frequent prevalence in documents. The most common way to remove such common English words is by applying “stop-list” at the preprocessing stage. Another common trick to apply for data preprocessing is variant unifying. Variant refers to different forms of the same word, for example, “go,” “goes,” “went,” “gone,” and “going.” This can be solved by stemming. This corresponds to the replacement of these words by a standard one. More sophisticated methods can not only be applied to the words with the same semantic meaning, but also can improve discrimination by considering word co-occurrence. The interested reader can refer to Chapter 10 in this book.

### 12.2.2 Image Features

Compared to text features, image features are usually large. Consider a modern image taken from a smartphone, in which the typical resolution is five mega-pixels (2592 × 1936). Without any pre-processing or compression, each image will be vectorized into a 5,018,112-dimensional Euclidean space. Typical large-scale image classification problems deal with millions or tens of millions of image samples. The storage for data of this size is nearly infeasible for most commodity desktop hardware. Moreover, such a huge dimensionality will introduce the curse of dimensionality. An increase in the number of parameters leads to instability and overfitting problems in model estimation [7]. Image data preprocessing and feature extraction are usually application-specific. Common techniques for preprocessing image data include downsampling, converting RGB data to 256-level gray scale, and normalizing data vectors to unit length. For particular applications such as face recognition or object recognition, cropping the desired region and aligning each face/object image will boost the classification performance significantly.

One unique problem in image classification compared to text is the so-called semantic ambiguity or semantic gap. Machine classification uses high level concepts or labels to categorize different data. A good semantic understanding of the feature space is critical for classification. Text is a form of natural language, and a special medium for humans to exchange knowledge. Therefore, the semantics of the feature representation is clear. Unfortunately, in the case of image data, the semantic knowledge is hard to interpret. In other words, samples with similar high level features may be further apart, while samples from different classes may cluster together [53], [83].

In the field of image processing, computer vision and pattern recognition, bridging the semantic gap between high-level concepts and low-level feature representations has been studied for a long time. The most effective way is to extract features in an application-specific way. There is no such feature extraction method that will work universally for all classification topics. Some example features include color, shape, texture and spatial layout information. A simple example is classifying “sky” and “sea.” These two concepts are difficult to distinguish due to their resemblance in color. However their spatial layout in the image can be a useful tool for classification: sky often appears at the top of image, while sea is at the bottom.

Another characteristic difficulty for image categorization is that samples from the same class usually contain large variations. A typical example is that of images of a person’s face. Humans can easily distinguish between different people without having seen the person before. However,
