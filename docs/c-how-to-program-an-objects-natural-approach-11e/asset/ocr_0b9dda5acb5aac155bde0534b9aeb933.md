As you implement the RSA algorithm, keep the following hints in mind:

+   - **Modular exponentiation:** Raising a plaintext message to a large exponent (e.g., 12237) results in enormous values that C++'s built-in integer types cannot represent. As you know, RSA encryption and decryption calculations perform both exponentiation and modulus operations. These can be combined using modular exponentiation to keep the RSA encryption and decryption calculations within manageable ranges. Define a function named `modularPow` that performs modular exponentiation. For the modular exponentiation algorithm, see the pseudocode at https://w.wiki/6bz9
+   - **Calculating the greatest common divisor:** The candidate values for e (**Step 4**) must be coprime with the totient—again, their only common factor is 1. To determine if two numbers are coprime, you'll need a function `gcd` that calculates the **greatest common divisor of two integers**. Your program should display all possible candidate values for e. You were asked to write a gcd function in Exercise 5.19.
+   - **Checking for prime numbers:** The RSA algorithm requires two prime numbers, p and q. Define a function `isPrime` to determine if an integer is prime. Use it to confirm that the p and q values the user entered are prime. Exercise 6.28 asked you to implement the Sieve of Eratosthenes to find prime values.

Your program also should define the following functions:

+   - A function to **encrypt a plaintext message M using the public key (e, n):**

```
int encrypt(int M, int e, int n);
```

+   - A function to **decrypt a ciphertext message C using the private key (d, n):**

```
int decrypt(int C, int d, int n);
```

+   - A function to **encrypt a string by calling the encrypt function for each character of the string and placing the results into a vector<int>:**

```
void encryptString(std::string_view plaintext,
    std::vector<int>& ciphertext, int e, int n);
```

+   - A function to **decrypt ciphertext from a vector<int>** by calling the decrypt function for each integer. The function should return the plaintext string:

```
std::string decryptString(
    std::vector<int>& ciphertext, int d, int n);
```

# References

For a video explanation of the RSA algorithm, see this two-part video presentation:

+   - The RSA Encryption Algorithm (1 of 2: Computing an Example):⁶⁵
+     https://www.youtube.com/watch?v=4zahvcJ9glg
+   - The RSA Encryption Algorithm (2 of 2: Generating the Keys):⁶⁶
+     https://www.youtube.com/watch?v=o0cTVTpuSPQ

65. Woo, Eddie (misterwootube). “The RSA Encryption Algorithm (1 of 2: Computing an Example),” November 4, 2014. https://www.youtube.com/watch?v=4zahvcJ9glg.
66. Woo, Eddie (misterwootube). “The RSA Encryption Algorithm (2 of 2: Generating the Keys),” November 4, 2014. https://www.youtube.com/watch?v=o0cTVTpuSPQ.