# Chapter 7 Methods: A Deeper Look

complete description of the class. Click the Methods link in the left-hand column to see a listing of the class's methods.

> Good Programming Practice 7.1
The online .NET Framework documentation is easy to search and provides many details about each class. As you learn each class in this book, you should review the class in the online documentation for additional information.

# 7.8 Case Study: Random-Number Generation

In this and the next section, we develop a nicely structured game-playing app with multiple methods. The app uses most of the control statements presented far in the book and introduces several new programming concepts.

There's something in the air of a casino that invites people—from the high rows at the plush mahogany-felt tables to the quarter near the one-armed bandits. It's the element of chance, the possibility that luck will convert a pocket of money into a mountain of wealth. The element of chance can be introduced in an app via an object of class Random (of Namespace System). Random can produce byte, int and double values. In the next examples, we use objects of class Random to produce random numbers.

# Secure Random Numbers

According Microsoft's documentation for class Random, the random values it produces are not completely random because a mathematical algorithm is used to select them, but they are sufficiently random for practical purposes. Such values should not be used, for example, to randomly select selected passwords. If your app requires so-cryptographically secure random numbers, use RNGryptoServiceProvider to produce random values:

```
https://msdn.microsoft.com/library/system.security.cryptography.
rngryptoserviceprovider
```

# 7.8.1 Creating an Object of Type Random

A new random-number generator object can be created with class Random (from the System namespace) as follows:

```
Random randomNumbers = new Random();
```

The Random object can then be used to generate random byte, int and double values—we discuss only int values here.

# 7.8.2 Generating a Random Integer

Consider the following statement:

```
int randomValue = randomNumbers.Next();
```

+   1. Class RNGryptoServiceProvider produces arrays of bytes. We discuss arrays in Chapter 8.