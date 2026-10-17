# CHAPTER 5  Scalars and Formatting

In Listing05_04, to use the `int()` function, you insert the rational number you want to convert to an integer. In this instance, the number (`$RandomNumber`) possesses a decimal precision of 14. If you are working with a dice game, such precision is not likely to be very useful. The `int()` function truncates the number for you. The output is as follows:

```
Random number without integer status:

4.77630615234375

Random number converted to an integer:

4

Press a key to continue...
```

# Range Problems and the rand() Function

To generate the random number shown in Listing05_04, you use the `rand()` function. By default, the return value of this function is a rational number in a range that is zero or greater and less than a whole number value of the digit you use as an argument. As Figure 5.5 illustrates, a problem results when you consider that a die has 6 dots. If you use an argument of 6 for the `rand()` function, the largest value the `rand()` function can generate is 5.99999999999999. This not quite 6. Likewise, a die has 1 to 6 dots; no face is blank. Such inconsistencies constitute a range problem.

![](bbox=[0.535, 0.489, 0.686, 0.703])

To solve the range problem, you shift the returned value of `rand()` function by one. Given the truncation that the `int()` function performs, if you add one to the value the `rand()` function generates and set the argument of `rand()` to 7, you then acquire numbers in the range of 1 to 6.

# Gargantuan Integers

Consider again the use of the `int()` function. In this case, the problem is that you want to do something like name the number of photons bombarding a rooftop on a sunny day. Listing05_05