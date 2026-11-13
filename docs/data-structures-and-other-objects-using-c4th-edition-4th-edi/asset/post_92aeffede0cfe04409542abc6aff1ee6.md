
have been produced. Other choices for the constants might not be so good.

For this project, design and implement a class that can generate a pseudorandom sequence in the manner described. The initial seed, multiplier, increment, and modulus should all be parameters of the constructor. There should also be a member function to permit the seed to be changed, and a member function to generate and return the next number in the pseudorandom sequence.

### 12 Add a new member function to the random number class of the previous project. The new member function generates the next pseudorandom number but does not return the number directly. Instead, the function returns this number divided by the modulus. (You will have to cast the modulus to a double number before carrying out the division; otherwise, the division will be an integer division, throwing away the remainder.)

The return value from this new member function is a pseudorandom double number in the range [0..1). (The square bracket, [, indicates that the range does include 0, but the rounded parenthesis, ), indicates that the range goes up to 1, without actually including 1.)

### 13 Run some experiments to determine the distribution of numbers returned by the new pseudorandom function from the previous project. Recall that this function returns a double number in the range [0..1). Divide this range into 10 intervals, and call this function one million times, producing a table such as this:

| Range | Number of Occurrences |
|---|---|
| [0.0 ... 0.1] | 99889 |
| [0.1 ... 0.2] | 100309 |
| [0.2 ... 0.3] | 100070 |
| [0.3 ... 0.4] | 99940 |
| [0.4 ... 0.5] | 99584 |
| [0.5 ... 0.6] | 100028 |
| [0.6 ... 0.7] | 99669 |
| [0.7 ... 0.8] | 100100 |
| [0.8 ... 0.9] | 100107 |
| [0.9 ... 1.0] | 100304 |

Run your experiment for different values of the multiplier, increment, and modulus. With good choices of the constants, you will end up with about 10% of the numbers in each interval. A pseudorandom number generator with this equal-interval behavior is called uniformly distributed.

### 14 This project is a continuation of the previous project. Many applications require pseudorandom number sequences that are not uniformly distributed. For example, a program that simulates the birth of babies can use random numbers for the birth weights of the newborns. But these birth weights should have a Gaussian distribution. In a Gaussian distribution, numbers are more likely to fall in intervals near the center of the overall distribution. The exact probabilities of falling in a particular interval can be computed from knowing two numbers: (1) the center of the overall distribution (called the median), and (2) a number called the standard deviation, which indicates how widely spread the distribution appears.

Generating a pseudorandom number sequence with an exact Gaussian distribution can be difficult, but there is a good way to approximate a Gaussian distribution using uniformly distributed random numbers in the range [0..1). The approach is to generate 12 uniformly distributed pseudorandom numbers, each in the range [0..1). These numbers are then combined to produce the next number in the Gaussian sequence. The formula to combine the numbers is given here, where sum is the sum of the 12 numbers and sd is the desired standard deviation:

```
Next number in the Gaussian sequence
= median + (sum - 6) × sd
```

Add a new member function to the random number class, which produces a sequence of pseudorandom numbers with approximate Gaussian distribution.

### 15 Write a class for rational numbers. Each object in the class should have two integer values that define the rational number: the numerator and the denominator. For example, the fraction 5/6 would have a denominator of 5 and a numerator of 6. Include a constructor with two arguments that can be used to set the numerator and denominator (forbidding zero in the denominator). Provide default values of zero for the numerator and one for the denominator. Overload the input and output operators. Numbers are to be read and written in the form 1/2, 32/15, 300/401, and so forth. Note that the numerator, the denominator, or both may contain a minus sign, so -1/2, 32/-15, and -300/-401 are possible. Include a function to normalize the values stored so that after normalization the denominator is positive and as small as possible. For example, after normalization, -4/-8 would be represented the same as -1/2.

Overload the usual arithmetic operators to provide addition, subtraction, multiplication, and division of two rational numbers. Overload the usual comparison operations to allow comparison of two rational numbers.

Hints: Two rational numbers a/b and c/d are equal if a*d equals c*b. For positive rational numbers, a/b is less than c/d, provided a*d is less than c*b.

### 16 Write a class to keep track of a balance in a bank account with a varying annual interest rate. The constructor will set both the balance and the annual interest rate to some initial values (with defaults of zero). The class should have member functions to change or retrieve the current balance or interest rate. There should also be functions to make a deposit (add to the balance) or a withdrawal (subtract from the balance). Finally, there should be a function that adds interest to the balance at the current interest rate. This function should have a parameter indicating how many years’ worth of interest are to be added (for example, 0.5 years indicates that the account should have six months’ interest added). Use the class as part of an interactive program that allows the user to determine how long an initial balance will take to grow to a given value. The program should allow the user to specify the initial balance, the interest rate, and whether there are additional yearly deposits.

### 17 Specify, design, and implement a class called date. Use integers to represent a date’s month, day, and year. Write a member function to increment the date to the next day. Include friend formats to display a date in both number and word format.

### 18 Specify, design, and implement a class called employee. The class has data members for the employee’s name, ID number, and salary based on an hourly wage. Member functions include computing the yearly salary and increasing the salary by a certain percentage. Add additional data members to store biweekly paycheck information and calculate overtime (for over 40 hours per week) for each paycheck.

### 19 Write a class for complex numbers. A complex number has the form a + bi, where a and b are real numbers and i is the square root of -1. We refer to a as the real part and b as the imaginary part of the number. The class should have two data members to represent the real and imaginary numbers; the constructor takes two arguments to set these members. Discuss and implement other appropriate operators for this class.

### 20 Write a class called fueler that can keep track of the fuel and mileage of a vehicle. Include private member variables to track the amount of fuel that the vehicle has consumed and the distance that the vehicle has traveled. You may choose whatever units you like (for example, fuel could be measured in U.S. gallons or Imperial gallons or liters), but be sure to document your choices at the point where you declare the variables. The class should have a constructor that initializes these variables to zero. Include a member function that can let reset both variables to zero. There are two different modification member functions to add a given amount to the total distance driven (one has a miles parameter, and the other has a kilometers parameter); similarly, there are three member functions to a given amount to the total fuel consumed (with different units for the amount of fuel). The class has two const member functions to retrieve the total distance driven (in miles or km), three functions for the fuel consumed (in U.S. gallons, Imperial gallons, or liters) and four for the fuel mileage (in U.S. mpg, Imperial mpg, km per liters, or liters per 100 km).
