
only links to the address. This should remind you of the call-by-reference in Chapter 2. These were, for the most part, limited pointers, which as you’ll recall, enabled us to both access and alter the passed variables from inside our subprograms. This gave us the power to use those values as if they were global variables, but with the increased plug-n-play ability of local variables, which makes pointers very useful, but also potentially dangerous. Thus, C# allows pointer manipulations, but only under the newly defined unsafe mode.

## Enabling unsafe Mode

Once a project is loaded into the .Net compiler, it becomes only a simple matter of altering that project’s build configuration to enable unsafe mode. From the folder labeled “View,” select the file titled “Solution Explorer” (see Screen Shot 4.1).

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_264_0.png)

A second side window will open; make sure to highlight the project rather than the file name. Select “Properties,” the third icon, depicted in that smaller window (see Screen Shot 4.2).

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_265_0.png)

Now go to the listing labeled “Configuration Properties.” Select “Build” from that sublist and click on the “False” value under the “Allow unsafe code blocks” From there, an arrow will appear—use it to select the “True” setting and press “Apply” (see Screen Shot 4.3).

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_265_1.png)

## Pointer Variables

Pointer variables, like all other types of variables, need to be declared, but because they require a location to point to, they also need to be assigned before they can be referenced. Pointers are also limited, like standard variables, by their data types and rules of naming. Thus, it stands to reason that pointers declared as integers can only point to standard variables that were also declared as integers, doubles with doubles, floats to floats, and characters to characters. The one key visual difference when declaring pointers is the insertion of the asterisk symbol (*), which is placed in front of the data type's reference. This asterisk tells the compiler that this data type is actually intended to declare pointer variables. The asterisk, in this case, is referred to as the dereferencing operator, and the variable is referred to as the dereference variable. The second step is to assign the pointer; this is done by making the pointer equal to the standard variable. An ampersand symbol (&) must precede the standard variable (ampersands are referred to as address operators). Remember, a pointer that has not been assigned has nothing to point to, and cannot be used (see Example 4.25). Note: There is also a void data type pointer, which is a generalized pointer that can be linked to any of the other data types. Void pointer data types are discussed later in this chapter.

### Example 4.25. Pointers.

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int* pointer1;
            int variable1 = 1;
            float* pointer2;
            float variable2 = 2.0f;
            double *pointer3;
            double variable3 = 3.01;
            char *pointer4;
            char variable4 = 'A';

            pointer1 = &variable1;
            pointer2 = &variable2;
            pointer3 = &variable3;
            pointer4 = &variable4;
            Console.WriteLine ("{0}    {1}", variable1, *pointer1);
            Console.WriteLine ("{0}    {1}", variable2, *pointer2);
            Console.WriteLine ("{0}    {1}", variable3, *pointer3);
            Console.WriteLine ("{0}    {1}", variable4, *pointer4);
        }
    }
}
```

We can also assign numeric values to pointers, but only after they have been assigned memory locations. Again, we'll use the equal sign to assign the values and the asterisk symbol to reference the pointer. You should note that since pointers place their new values in the memory locations used by standard variables, any previous information is overwritten.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_267_0.png)

> "I just got this new pointer VISA—it has my name on it, but the charges are linked to someone else's account."
> "Are you sure that's legal?"
> "Well, not always, I have to use it in unsafe counties."

Pointers can also assign locations to other pointers—see the code in Example 4.26.

### Example 4.26. Assigning values and memory locations to pointers.

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int* pointer1, pointer2;
            // Warning, pointer3 is not an actual pointer!
            int variable1 = 1, pointer3;
            // Assigning a pointer to a value
            pointer1 = &variable1;
            // Pointer to pointer assignments DO NOT require the asterisk.
            pointer2 = pointer1;
            // Pointers can also pass values to variables.
            pointer3 = *pointer2;
            Console.WriteLine("{0}  {1}  {2}  {3}",
                variable1, *pointer1, *pointer2, pointer3);

            *pointer1 = 20;  // the value inside that address is now 20.

            Console.WriteLine("{0}  {1}  {2}  {3}",
                variable1, *pointer1, *pointer2, pointer3);
        }
    }
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_268_0.png)

### The Keyword null

The keyword null is the only value that can be assigned to an unassigned pointer without causing an error. The null statement is also useful when passing meaningless values to a generalized function as in MyFunction (SomeNumber, null); where a second value is not required when the first value represents a short-circuit event. The null value works in basically the same manner as did the NULL value in C++, except now it's actually a keyword.

## Call-By-Reference Values with Pointer Arguments

As you'll remember from Chapter 2, we were able to write function calls as both calls-by-value and calls-by-reference, but calls-by-reference also let us change the values of the original variables. You should also recall (from our introduction to pointers) that calls-by-reference are actually limited forms of pointers. This makes it possible to rewrite those programs so that they use actual pointer notation without significantly changing those programs (see Example 4.27)

### Example 4.27. Calls-by-reference with pointer arguments.

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            string input;
            char race = 'y';
            int winner, number1 = 0, number2 = 0, number3 = 0;

            Console.WriteLine("Let's have a horse race.\n"
                + "To play select one of the horses below");

            while (char.ToUpper (race) != 'N') {
                Console.WriteLine("(1) for Whitefire\n"
                    + "(2) for The Train and, \n"
                    + "(3) for Noisy Glue");

                input = Console.ReadLine();

                the_race(&number1, &number2, &number3);
                tie_breaker(&number1, &number2);
                tie_breaker(&number2, &number3);
                tie_breaker(&number1, &number3);

                winner = the_winner(&number1, &number2, &number3);
                Console.Write("And the winner is ");

                if (winner == '1')
                    Console.WriteLine("Whitefire");
                else if (winner == '2')
                    Console.WriteLine("The Train");
                else
                    Console.WriteLine("Noisy Glue");

                Console.Write("Would you like to play again (Y/N)?");
                input = Console.ReadLine();
                race = char.Parse(input);
            }
        }

        static unsafe void the_race(int *number1, int *number2,
            int *number3) {
            Random rnd = new Random();

            *number1 = (int)(rnd.NextDouble() * 100);
            *number2 = (int)(rnd.NextDouble() * 100);
            *number3 = (int)(rnd.NextDouble() * 100);
            Console.Write(".");
        }

        static unsafe void tie_breaker(int *num1, int *num2) {
            if (*num1 == *num2)
                *num2 = *num2 - 1;
            Console.Write(",");
        }

        static unsafe char the_winner(int *num1, int *num2, int *num3) {
            char winner;
            if (*num1 > *num2 && *num1 > *num3)
                winner = '1';
            else if (*num2 > *num1 && *num2 > *num3)
                winner = '2';
            else winner = '3';
            Console.Write(".");

            return(winner);
        }
    }
}
```

## Pointer Arithmetic

Pointer arithmetic is simply variable arithmetic as applied to pointers (note: asterisks are required). In pointer arithmetic, pointers are used like variables to add, subtract, multiply, divide, and find the remainder of stored values. Pointers can also be used with shorthand notation and the incrementing and decrementing operators (incrementing & decrementing operators also require the insertion of parentheses—see Examples 4.28 and 4.29).

### Example 4.28. Arithmetic with pointers.

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int number1 = 0, number2 = 0;
            int* pointer1 = &number2;

            number1 = number1 + 10;       // Addition
            *pointer1 = *pointer1 + 10;
            Console.WriteLine("{0}    {1}", number1, number2);

            number1 = number1 - 1;       // Subtraction
```
