as the input variable; the mathematical transformations that will be applied to this variable will produce the features.

Two important and widely used techniques for speech recognition will be presented in this section due to its relevance to this field. Linear Predictive Coding, or LPC, is a predictive technique in which a linear combination of some K coefficients and the last K samples from the signal will predict the value of the next one; the K coefficients will represent the distinctive features. The following section will explain the LPC method in detail.

# 3.1 Linear Predictive Coding (LPC)

LPC is one of the most advanced analytical techniques used in the estimation of patterns, based on the idea that the present sample can be predicted from a linear combination of some past samples, generating a spectral description based on short segments of signal considering a signal s[n] to be a response of an all-pole filter excitation u[n].

![](bbox=[0.25, 0.48, 0.75, 0.7])

Fig. 1. LPC model of speech.

Figure 1 shows the model the LPC is based on, considering that the excitation u[n] is the pattern waiting to be recognized. The transfer function of the filter is described as [3]:

H(z) = S(z)/U(Z) = G / (1 - sum_{k=1}^{p} a_k z^{-k}) = G / A(z)   (1)

where G is a gain parameter, a_k are the coefficients of filter and p determines the order of the filter. In Figure 1, the samples s[n] are related to the excitation u[n] by the equation:

s[n] = sum_{k=1}^{p} a_k s[n - k] + G u[n]   (2)

Considering that the linear combination of past samples is calculated by using an estimator \bar{s}[n] which is denoted by:

\bar{s}[n] = sum_{k=1}^{p} a_k s[n - k]   (3)