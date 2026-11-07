+   a) Write a program that reads a nonnegative integer and computes and prints its factorial. [Note: Factorial values grow quickly beyond what you can represent with C++’s fundamental integer types. Consider using Boost Multiprecision’s `cpp_int` type here, as shown in Section 3.14.]

+   b) Write a program that estimates the value of the mathematical constant $e$ by using the formula:
+   
+   $$e = 1 + \frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \cdots$$
+   
+   Prompt the user for the desired accuracy of $e$ (i.e., the number of terms in the summation).

+   c) Write a program that computes the value of $e^x$ by using the formula:
+   
+   $$e^x = 1 + \frac{x}{1!} + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots$$
+   
+   Prompt the user for the desired accuracy of $e$ (i.e., the number of terms in the summation).

# 3.26 **(Enforcing Privacy with Cryptography)**

The explosive growth of Internet communications and data storage on Internet-connected computers has greatly increased privacy concerns. The field of cryptography is concerned with coding data to make it difficult (and hopefully—with the most advanced schemes—impossible) for unauthorized users to read. In this exercise, you’ll investigate a simple scheme for encrypting and decrypting data. Later in the book, you’ll learn sophisticated secret-key and public-key cryptography. A company that wants to send data over the Internet has asked you to write a program that will encrypt the data so that it may be transmitted more securely. All the data is transmitted as four-digit integers. Your application should read a four-digit integer entered by the user and encrypt it as follows: Replace each digit with the result of adding 7 to the digit and getting the remainder after dividing the new value by 10. Then swap the first digit with the third, and swap the second digit with the fourth. Then print the encrypted integer. Write a separate application that inputs an encrypted four-digit integer and decrypts it (by reversing the encryption scheme) to form the original number.

# 3.27 **(Other Boost Multiprecision Arithmetic Operations)**

Section 3.14 introduced the Boost Multiprecision library’s `cpp_int` class and used `cpp_int` objects with the addition, subtraction and multiplication operators. You also may use division (`/`) and modulus (`%`) operators. In addition, the Boost Multiprecision library provides many functions that perform common arithmetic calculations, such as `pow` for raising a value to a specified power or `sqrt` for calculating the square root of a number. To use the `sqrt` and `pow` functions, add the following using declarations before `main`:²¹

```
using boost::multiprecision::pow;
using boost::multiprecision::sqrt;
```