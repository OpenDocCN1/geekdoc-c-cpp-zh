over the Internet.<sup>73,74,75</sup> Industrial-strength RSA works with enormous prime numbers consisting of hundreds of digits. The sheer amount of time required to factor the product of those primes—even for the most powerful supercomputers in use today— is a key reason why RSA is so secure. Public-key cryptography also is used to secure the blockchain technology behind cryptocurrencies like Bitcoin.<sup>76</sup> The RSA Public-Key Cryptography case-study exercise at the end of Chapter 9 presents the RSA algorithm.

# Overview of This Example

This example’s task to execute is defined by the `getFactors` function (lines 27–68), which determines whether a number is prime<sup>77</sup> and, if not, determines its prime factors. Each thread in this program executes until `getFactors` returns its result—a `std::tuple` containing the task name, the number `getFactors` processed, a bool indicating whether the number is prime and a vector of the number’s factors. To ensure that our tasks run for at least a few seconds each, we used two 19-digit numbers, including a prime value from the University of Tennessee Martin’s Prime Pages website.<sup>78</sup> Its prime-number research includes lists of prime values by their numbers of digits.

Figure 17.12 consists of the following functions:

+   - Function `id` (lines 13–17) converts a unique `std::thread::id` to a `std::string`.
+   - Function `getFactors` (lines 27–68) attempts to find an integer’s factors.
+   - Function `proveFactors` (lines 71–90) confirms that a given set of prime factors, when multiplied together, reproduces a corresponding non-prime value.
+   - Function `displayResults` (lines 93–117) displays a task’s results.
+   - Function `main` (lines 119–133) launches the `getFactors` tasks, waits for them to complete, then displays their results.

We’ve split this program into pieces for discussion purposes. After the program, we show sample outputs. In Fig. 17.12, lines 3–10 `#include` the headers used in this program.

+   73. “RSA (Cryptosystem).” Accessed April 18, 2023. https://en.wikipedia.org/wiki/RSA_(cryptosystem).
+   74. “RSA Algorithm.” Accessed April 18, 2023. https://simple.wikipedia.org/wiki/RSA_algorithm.
+   75. K. Moriarty, B. Kaliski, J. Jonsson and A. Rusch, “PKCS #1: RSA Cryptography Specifications Version 2.2,” November 2016. Accessed April 18, 2023. https://tools.ietf.org/html/rfc8017.
+   76. Sarah Rothrie, “How Blockchain Cryptography Is Fighting the Rise of Quantum Machines,” December 28, 2018. Accessed April 18, 2023. https://coincentral.com/blockchain-cryptography-quantum-machines/.
+   77. “Primality Test.” Accessed April 18, 2023. https://en.wikipedia.org/wiki/Primality_test.
+   78. “Index: Numbers.” Accessed April 18, 2023. https://www.mutm.edu/curios/index.php.