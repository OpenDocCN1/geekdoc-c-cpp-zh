# 1014 Chapter 23 Asynchronous Programming with async and await

# Exercises

23.6 Investigate other compute-intensive calculations, then modify the example of Fig. 23.1 to perform a different compute-intensive calculation asynchronously.

23.7 Modify the example of Fig. 23.3 to process the results using the array returned by the Task produced by Task method when awaitAll.

23.8 Investigate other web services at a site like http://www.programmableweb.com. Locate a REST service that returns XML, then modify the example of Fig. 23.4 to invoke the web service asynchronously using the methods of class `HttpClient`. Parse the results using LINQ to XML, then display the results as as appropriate for the type of data returned.

23.9 You have noticed that the prime-number example in Fig. 23.6 produces prime numbers rapidly. although that is, the speed of displaying the results on the screen slows down the program, not the ability of the computer to determine the prime number. Reimplement the example of Fig. 23.6 with a compute bound algorithm such as the recursive Fibonacci calculation of Fig. 23.1. When you run the app, the Fibonacci numbers get higher; the calculation slows dramatically, slowing the updates of the ProgressBar and the TextBox that shows the calculation results. This calculation is bound, the overall speed of the app on your processor—you want to decrease or increase the large Fibonacci number the app calculation accordingly. For example, on our computer the Fibonacci of 47 takes minutes to calculate.

23.10 Visit https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes to learn more about the Sieve of Eratosthenes. The algorithm as implemented in Fig. 23.6 is inefficient, because it keeps eliminating multiples of primes even after the array already represents all primes up to the maximum value less than or equal to the square root of the maximum value. Make the following modifications to Fig. 23.6:

+   a) Update the algorithm to eliminate multiples of primes that are less than or equal to the square root of the maximum value.
b) Modify the code that updates the ProgressBar and percentage Label so that they they indicate the progress of the Sieve of Eratosthenes algorithm, rather than the progress of checking each number in the range is prime.