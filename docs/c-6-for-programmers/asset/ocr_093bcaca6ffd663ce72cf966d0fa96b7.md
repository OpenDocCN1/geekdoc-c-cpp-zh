# async Method FindPrimes

The async method FindPrimes implements the Sieve of Eratosthenes algorithm, displays the primes that are found and updates the progressBar and percentage completion. Line 50 initially sets primeCount to 0 to indicate that no primes have been found yet. Lines 53–66 iterate through the values from 2 up to, but not including, the maximum entered by the user. For each value, line 56 launches an async Task to determine whether that value is prime and awaits the Task's result. When that result is returned, if it's true, line 58 increments primeCount to indicate that a prime number was found and line 59 appends that number's string representation to the primesTextBox's text—thus displaying one of the intermediate results. Regardless of whether a value is prime, lines 62–64 calculate the percentage of the loop that has completed so far and display that percentage, and line 65 updates the progressBar's Value.

At any point during the execution of FindPrimes, the user could click the app's Cancel Button, in which case property Canceled will be set to true and the loop will terminate early. If this occurs, lines 69–72 display "Canceled" in the primesTextBox.

# Method IsPrime

Method IsPrime (lines 81–99) is called by async method FindPrimes to perform part of the Sieve of Eratosthenes. IsPrime tests whether its value argument is prime by checking the corresponding element in array primes (line 85). If value is prime, lines 88–91 set to false the primes elements at all indices that are multiples of value, then line 93 returns true to indicate that value is prime; otherwise, the method returns false.

# Method cancelButton_Click

When the user clicks the Cancel button, method cancelButton_Click (lines 102–107) sets property Canceled to true, then enables the Get Primes Button and disables the Cancel Button. When the condition at line 53 is evaluated next, the loop in method FindPrimes terminates.

# 21.8 Wrap-Up

In this chapter, you learned how to use the async modifier, await operator and Tasks to perform long-running or compute-intensive tasks asynchronously. You learned that tasks that proceed independently of one another are said to execute asynchronously and are referred to as asynchronous tasks.

We showed that multithreading enables threads to execute concurrently with other threads while sharing application-wide resources such as memory and processors. To take full advantage of multicore architecture, we wrote applications that processed tasks asynchronously. You learned that asynchronous programming is a technique for writing apps containing tasks that can execute asynchronously, which can improve app performance and GUI responsiveness in apps with long-running or compute-intensive tasks.

To provide a convincing demonstration of asynchronous programming, we presented several apps:

+   - The first showed how to execute a compute-intensive calculation asynchronously in a GUI app so that the GUI remained responsive while the calculation executed.