numbers. The extra variable max is not strictly necessary, but it makes thinking about the problem and its solution easier.

Something to think about: Do you want a series of if statements or one large multiway if/else construct?

```
if (n1 >= n2 && n1 >= n3 && n1 >= n4 && n1 >= n5)
    std::cout << "The maximum is " << n1 << '\n';
else if ( n2 >= n1 && n2 >= n3 &&
          // the rest omitted . . .
```

This will work, but this logic is much more complicated and less efficient (every >>= and && operation requires a few machine cycles to execute). Since it is more complicated, it is more difficult to write correctly, in addition to being more code to type in. It is easy to use > by mistake instead of >=, which will not produce the correct results. Also, if you use this more complicated logic and decide later to add more variables, you will need to change all of the if conditions in your code and, of course, make sure to modify each one of the conditions correctly. If you implement the simpler strategy outlined before, you need only add one simple if statement for each additional variable.

Chapter 6 introduces loops, the ability to execute statements repeatedly. You easily can adapt the first approach to allow the user to type in as many numbers as they like and then have the program report the maximum number the user entered. The second approach with the more complex logic cannot be adapted in this manner. With the first approach you end up with cleaner, simpler logic, a more efficient program, and code that is easier to extend.

# 5.9 Errors in Conditional Statements

Consider Listing 5.18 (badequality.cpp).

```
Listing 5.18: badequality.cpp

#include <iostream>

int main() {
   int input;
   std::cout << "Please enter an integer:";
   std::cin >> input;
   if (input = 2)
      std::cout << "two\n";
   std::cout << "You entered " << input << '\n';
}
```

Listing 5.18 (badequality.cpp) demonstrates a common mistake—using the assignment operator where the equality operator is intended. This program, when run, always prints the message “two” and insists the user entered 2 regardless of the actual input. Recall from Section 4.3 that the assignment expression has a value. The value of an assignment expression is same as the value that is assigned; thus, the expression

```
input = 2
```

has the value 2. When you consider also that every integer can be treated as a Boolean value (see Section 5.1) and any non-zero value is interpreted as true, you can see that the condition of if statement