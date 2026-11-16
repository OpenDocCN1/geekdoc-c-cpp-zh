ing described in the above sections and confirm the result using our formalization in HOL. In this specific case, we detected the problem when trying to prove the erroneous assumption stating that the channel capacity is achieved when all input symbols have non-zero probabilities.

To the best of our knowledge, this is the first time the properties of mixes have been analyzed using theorem proving. This is obviously not a large application and can be extended to reason about MIX networks and other anonymity networks in general. However this serves as an example to illustrate the usefulness of the framework presented in book. Thanks to the rich formalization of information theory, we were able to analyze the MIX of this application within one week of human effort and using around 500 lines of HOL4 code.

# 11.3 ONE-TIME PAD

The one-time pad is a simple yet solid encryption system that provides, if used correctly, an unbreakable security. The encryption is performed by modular addition of every character of the plaintext with a character from a secret random key of at least the same length as the original message. If the key is truly random and never reused in whole or in part, then it can be proven that the one-time pad encryption provides a perfect security. We formally prove this property within the HOL4 theorem prover using the higher-order-logic framework proposed in this book. The one-time pad

Figure 5. A Russian one-time pad, captured by MI5

![](bbox=[0.37, 0.59, 0.63, 0.89])