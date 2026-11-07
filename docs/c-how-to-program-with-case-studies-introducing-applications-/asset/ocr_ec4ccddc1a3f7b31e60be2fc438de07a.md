calculations within manageable ranges. Define a function named `modularPow` that performs modular exponentiation. For the modular exponentiation algorithm, see the pseudocode at

https://en.wikipedia.org/wiki/Modular_exponentiation#Memory-efficient_method

+   - **Calculating the greatest common divisor:** The candidate values for e (*Step 4*) must be coprime with the totient—again, their only common factor is 1. To determine if two numbers are coprime, you’ll need a **function gcd** that calculates the **greatest common divisor of two integers**. Your program should display all possible candidate values for e. You are asked to write a gcd function in Exercise 5.29.
+   - **Checking for prime numbers—**The RSA algorithm requires two prime numbers, p and q. You should define a **function `isPrime` that determines if an integer is indeed a prime number**—use it to confirm that the p and q values the user entered are prime. Exercise 6.30 asked you to implement the Sieve of Eratosthenes to find prime values.

Your program also should define the following functions:

+   - A **function to encrypt a plaintext message M using the public key (e, n):**
+   
+     ```text
+     int encrypt(int M, int e, int n);
+     ```
+   - A **function to decrypt a ciphertext message C using the private key (d, n):**
+   
+     ```text
+     int decrypt(int C, int d, int n);
+     ```
+   - A **function to encrypt a string by calling the encrypt function for each character of the string and placing the results into an integer array:**
+   
+     ```text
+     void encryptString(
+         char* plaintext, int ciphertext[], int e, int n);
+     ```
+   - A **function to decrypt ciphertext from an integer array by calling the decrypt function for each integer and placing the results into a char array.** The size parameter represents the number of characters that were encrypted. Be sure to terminate the string in `decryptedPlaintext` with a null character (`'\0'`):
+   
+     ```text
+     void decryptString(int ciphertext[],
+         char decryptedPlaintext[], size_t size, int d, int n);
+     ```

# References

For a nice video explanation of the RSA algorithm, see the following two-part video presentation:

+   - The RSA Encryption Algorithm (1 of 2: Computing an Example):
+   
+     https://www.youtube.com/watch?v=4zahvCJ9JgI
+   - The RSA Encryption Algorithm (2 of 2: Generating the Keys):