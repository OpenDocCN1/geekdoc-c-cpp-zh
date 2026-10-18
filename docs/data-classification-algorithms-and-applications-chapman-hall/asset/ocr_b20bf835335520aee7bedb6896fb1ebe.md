several probabilistic discriminative models, including Logistic Regression, a type of generalized linear models [23], and Conditional Random Fields.

In this chapter, we introduce several fundamental models and algorithms for probabilistic classification, including the following:

+   - **Naive Bayes Classifier.** A Naive Bayes classifier is a simple probabilistic classifier based on applying Bayes’ theorem with strong (naive) independence assumptions. A good application of Naive Bayes classifier is document classification.
+   
+   - **Logistic Regression.** Logistic regression is an approach for predicting the outcome of a categorical dependent variable based on one or more observed variables. The probabilities describing the possible outcomes are modeled as a function of the observed variables using a logistic function.
+   
+   - **Hidden Markov Model.** A Hidden Markov model (HMM) is a simple case of dynamic Bayesian network, where the hidden states are forming a chain and only some possible value for each state can be observed. One goal of HMM is to infer the hidden states according to the observed values and their dependency relationships. A very important application of HMM is part-of-speech tagging in NLP.
+   
+   - **Conditional Random Fields.** A Conditional Random Field (CRF) is a special case of Markov random field, but each state of node is conditional on some observed values. CRFs can be considered as a type of discriminative classifiers, as they do not model the distribution over observations. Name entity recognition in information extraction is one of CRF’s applications.

This chapter is organized as follows. In Section 3.2, we briefly review Bayes’ theorem and introduce Naive Bayes classifier, a successful generative probabilistic classification. In Section 3.3, we describe a popular discriminative probabilistic classification logistic regression. We therefore begin our discussion of probabilistic graphical models for classification in Section 3.4, presenting two popular probabilistic classification models, i.e., hidden Markov model and conditional random field. Finally, we give the summary in Section 3.5.

# 3.2  Naive Bayes Classification

The Naive Bayes classifier is based on the Bayes’ theorem, and is particularly suited when the dimensionality of the inputs is high. Despite its simplicity, the Naive Bayes classifier can often achieve comparable performance with some sophisticated classification methods, such as decision tree and selected neural network classifier. Naive Bayes classifiers have also exhibited high accuracy and speed when applied to large datasets. In this section, we will briefly review Bayes’ theorem, then give an overview of Naive Bayes classifier and its use in machine learning, especially document classification.

# 3.2.1  Bayes’ Theorem and Preliminary

A widely used framework for classification is provided by a simple theorem of probability [5, 11] known as Bayes’ theorem or Bayes’s rule. Before we introduce Bayes’ Theorem, let us first review two fundamental rules of probability theory in the following form:

$$p(X) = \sum_Y p(X,Y) \tag{3.1}$$

$$p(X,Y) = p(Y\mid X)p(X). \tag{3.2}$$