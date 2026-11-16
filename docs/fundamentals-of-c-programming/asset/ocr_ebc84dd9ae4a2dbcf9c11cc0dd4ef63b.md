```
if (num1 % i == 0 && num2 % i == 0)
   largestFactor = i; // Found larger factor
std::cout << largestFactor << '\n';
}
```

Listing 9.8 (gcdproc.cpp) implements a straight-forward but naive algorithm that seeks potential factors by considering every integer less than the smaller of the two values provided by the user. This algorithm is not very efficient, especially for larger numbers. Its logic is easy to follow, with no deep mathematical insight required. Soon we will see a better algorithm for computing GCD.

If we need to compute the GCD from several different places within our program, we should package the code in a function rather than copying it to multiple places. The following code fragment defines a C++ function that computes the greatest common divisor of two integers. It determines the largest factor (divisor) common to its parameters:

```
int gcd(int num1, int num2) {
   // Determine the smaller of num1 and num2
   int min = (num1 < num2) ? num1 : num2;
   // 1 is definitely a common factor to all ints
   int largestFactor = 1;
   for (int i = 2; i <= min; i++)
      if (num1 % i == 0 && num2 % i == 0)
         largestFactor = i; // Found larger factor
   return largestFactor;
}
```

This function is named gcd and expects two integer arguments. Its formal parameters are named num1 and num2. It returns an integer result. Its body declares three local variables: min, largestFactor, and i (i is local to the for statement). The last line in its body is a return statement. A return statement is required for functions that return a value. A void function is not required to have a return statement. If a void function does have a return statement, it must simply consist of return followed by a semicolon (in other words, it cannot return a value, like gcd's return statement does). A void function that does not contain a return statement simply returns at the end of its body.

Recall from Section 6.5 that local variables have meaning only within their scope. This means that when you write a function can name a local variable without fear that its name may be used already in another part of the program. Two different functions can use local variables named x, and these are two different variables that have no influence on each other. Anything local to a function definition is hidden to all code outside that function definition.

Since a formal parameter is a local variable, you can reuse the names of formal parameters in different functions without a problem.

It may seem strange that we can use the same name in two different functions within the same program to refer to two distinct variables. The block of statements that makes up a function definition constitutes a context for local variables. A simple analogy may help. In the United States, many cities have a street named Main Street; for example, there is a thoroughfare named Main Street in San Francisco, California. Dallas, Texas also has a street named Main Street. Each city and town provides its own context for the use of the term Main Street. A person in San Francisco asking "How do I get to Main Street?" will receive the directions to San Francisco's Main Street, while someone in Dallas asking the same question will receive Dallas-specific instructions. In a similar manner, assigning a variable within a function block localizes its identity to that function. We can think of a program's execution as a person traveling around the U.S. When in San Francisco, all references to Main Street mean San Francisco's Main Street, but when the traveler