# CHAPTER 21

# CHAOTIC NEURAL NETWORKS AND BEYOND

KAZUYUKI AIHARA*,‡, TAIJI YAMADA† and MAKITO OKU*

*Institute of Industrial Science, University of Tokyo,
4-6-1 Komaba, Meguro-ku, Tokyo 153-8505, Japan
†AIHARA Electrical Engineering Co., Ltd.

A chaotic neuron model which is closely related to deterministic chaos observed experimentally with squid giant axons is explained, and used to construct a chaotic neural network model. Further, such a chaotic neural network is extended to different chaotic models such as a large-scale memory relation network, a locally connected network, a vector-valued network, and a quaternionic-valued neuron.

+   1. Introduction .......................................................... 259
+   2. A Model of Chaotic Neural Networks ................................. 260
+   3. Large-scale Chaotic Neural Networks with Memory Relation Network Structure ........ 262
+   4. Traveling Waves in Locally Connected Chaotic Neural Networks and Vector-valued Chaotic Neural Networks .... 265
+   5. A Quaternionic-valued Chaotic Neuron Model ......................... 267
+   6. Conclusions ............................................................ 268
+   Acknowledgments .......................................................... 268
+   References ............................................................... 268

# 1.  Introduction

Professor Leon Chua has been making great contributions to dynamical systems theory and its applications, including chaotic electrical circuits such as Chua’s circuit (e.g., Chua et al. [1]), cellular neural networks [2], and memristors [3] that may realize the implementation of plastic circuits similar to biological neural networks. Thus, his achievements cover many disciplines such as nonlinear science, engineering, and neuroscience.

In this chapter, we present another approach that combines chaotic dynamics with neural networks, namely the modelling of chaotic neural networks [4,5].

The brain is a large-scale nonlinear network composed of neurons and synapses. A seminal mathematical model of a neuron was proposed by McCulloch and Pitts in 1943 [6]. This model uses binary output values (0 and 1, that is, non-firing and firing, respectively), with discrete-time updating, which makes its operation similar to that of a logic element.

The actual behavior of biological neurons is far more complicated and dynamic than that of