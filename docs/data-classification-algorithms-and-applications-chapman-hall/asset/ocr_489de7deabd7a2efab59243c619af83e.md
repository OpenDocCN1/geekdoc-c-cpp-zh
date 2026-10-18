# Chapter 9

# A Survey of Stream Classification Algorithms

**Charu C. Aggarwal**

*IBM T. J. Watson Research Center*
*Yorktown Heights, NY 10598*
`charu@us.ibm.com`

+   9.1  Introduction .......................................................... 245
+   9.2  Generic Stream Classification Algorithms ............................... 247
+       9.2.1  Decision Trees for Data Streams .................................. 247
+       9.2.2  Rule-Based Methods for Data Streams .............................. 249
+       9.2.3  Nearest Neighbor Methods for Data Streams ......................... 250
+       9.2.4  SVM Methods for Data Streams ...................................... 251
+       9.2.5  Neural Network Classifiers for Data Streams ....................... 252
+       9.2.6  Ensemble Methods for Data Streams ................................ 253
+   9.3  Rare Class Stream Classification ....................................... 254
+       9.3.1  Detecting Rare Classes ............................................ 255
+       9.3.2  Detecting Novel Classes ........................................... 255
+       9.3.3  Detecting Infrequently Recurring Classes .......................... 256
+   9.4  Discrete Attributes: The Massive Domain Scenario ....................... 256
+   9.5  Other Data Domains ...................................................... 262
+       9.5.1  Text Streams ....................................................... 262
+       9.5.2  Graph Streams ...................................................... 264
+       9.5.3  Uncertain Data Streams ............................................. 267
+   9.6  Conclusions and Summary .................................................. 267
+   Bibliography ................................................................. 268

# 9.1  Introduction

Advances in hardware technology have led to the increasing popularity of data streams [1]. Many simple operations of everyday life, such as using a credit card or the phone, often lead to automated creation of data. Since these operations often scale over large numbers of participants, they lead to massive data streams. Similarly, telecommunications and social networks often contain large amounts of network or text data streams. The problem of learning from such data streams presents unprecedented challenges, especially in resource-constrained scenarios.

An important problem in the streaming scenario is that of data classification. In this problem, the data instances are associated with labels, and it is desirable to determine the labels on the test instances. Typically, it is assumed that both the training data and the test data may arrive in the form of a stream. In the most general case, the two types of instances are mixed with one another. Since the test instances are classified independently of one another, it is usually not difficult to perform the real-time classification of the test stream. The problems arise because of the fact that the training