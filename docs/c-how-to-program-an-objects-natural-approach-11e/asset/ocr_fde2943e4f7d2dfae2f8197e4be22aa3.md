know the private key required to decrypt the ciphertext. Use brute-force computing techniques to find n’s prime factors p and q. Then, do the calculations necessary to recover d and decrypt the message.

# 9.39 *(Challenging Research Project: Elliptic Curve Cryptography)*

[Note: Portions of this research project require sophisticated mathematics.] Exercise 9.34 presented public-key cryptography with RSA—the world’s most widely used cryptographic system. RSA encryption could soon be broken due to rapidly increasing computing power and breakthroughs in prime-factorization algorithms.⁷¹

Elliptic Curve Cryptography (ECC)⁷²,⁷³—based on complex mathematical properties of elliptic curves—is emerging as a powerful RSA alternative. It can achieve the same level of security with smaller keys—and extraordinary levels of security with larger ones. ECC uses significantly less processor bandwidth, storage and energy than RSA, so it’s widely used for limited-resource systems, such as IoT devices, limited-battery-power mobile phones and cryptocurrency networks like Bitcoin and Ethereum. ECC is especially popular for securing exponentially growing Internet communications. Its lower energy requirements are appealing at a time when the enormous energy requirements of cryptocurrency networks are causing concern about their future growth and the growth of other blockchain-based solutions.

The mathematics of ECC is much more complex than that of RSA. Although that makes ECC systems more challenging to build and maintain, they are far more difficult to break than RSA. Public-key cryptography depends on finding functions that are easy to do in one direction but extremely difficult to do (time-wise) in reverse—these are called trapdoor functions. For example, in RSA, it’s relatively fast and easy to multiply two large prime numbers to produce their non-prime product. However, it’s extremely difficult and time-consuming to go in the reverse direction—finding a huge number’s prime factors could take millions of years of computing time. By some estimates, breaking ECC systems could take time comparable to the length of the universe.⁷⁴

Research elliptic curve cryptography online and address each of the following:

+   a) Explain how ECC uses elliptic curve equations of the following form to find public-key/private-key pairs:
+   
+   \(y^2 = x^3 + ax + b\)
+   
+   b) Find a C++ ECC implementation on GitHub and study the code.
+   c) Which elliptic curve does the implementation use?
+   d) Explain the “easy” portion of the trapdoor function this implementation uses.
+   e) Explain what the “hard” portion of this trapdoor function would require to break its ECC system.
+   f) Briefly explain ECC’s known vulnerabilities.

71. Yan, Bao et al. “Factoring integers with sublinear resources on a superconducting quantum processor,” December 23, 2022. Accessed April 18, 2023. https://arxiv.org/pdf/2212.12372.pdf.

72. “Elliptic-curve cryptography.” Accessed April 18, 2023. https://en.wikipedia.org/wiki/Elliptic-curve_cryptography.

73. Matt Rickard, “Elliptic Curve Cryptography for Beginners.” March 27, 2022. Accessed April 18, 2023. https://matt-rickard.com/elliptic-curve-cryptography.

74. Ryan Sanders, “Elliptic Curve Cryptography: What is it? How does it work?” November 29, 2022. Accessed May 7, 2023. https://www.keyfactor.com/blog/elliptic-curve-cryptography-what-is-it-how-does-it-work/.