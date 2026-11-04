
> **Note**
>
> We could also have replaced that user-defined function with the predefined function `Math.Sqrt()`.

## Writing Functions as Black Boxes

The *black box theory* is simply a concept that stresses the idea that most, if not all, functions should be thought of as independent or self-containing subprograms. It also reasons that the coding used to construct such a function does not need to be studied or known by a programmer who only wants to invoke that function. Thus, the only information needed to access a function is the proper passing variables and the knowledge of what would be returned by the function. This is analogous to being able to drive a car, but not knowing how to repair the engine. This is actually the norm in C#, since all predefined functions are black boxes to most programmers and the idea of enhancing them would literally force us to open them up and redesign them to some new standard (which unfortunately is usually necessary in game programming). Of course, if you were to write your own user-defined functions, you'd certainly know how each one of them worked.

Creating a black box style function requires or restricts us to the use of encapsulated controls. This, of course, means that you must avoid using global variables and that you must include comments with every prototype to alert any other programmer to the variable settings and to their results. In addition, you should keep in mind that in later chapters, we'll be both reading and writing to user-defined functions from separate files, thus creating a real need for detailed comments explaining what these different function calls do.

> **Applying the black box approach to Example 2.40**
>
> Let's assume that you didn't really understand the second portion of the last example, but you used the square root function anyway. While it is a bit disheartening to the mathematician in me, this will not affect the way the program executes that data, and in fact, actually makes my point. If however, that coding piqued your interest then here's a quick overview of the mathematics (see Example 2.41).

### Example 2.41. The square root function explained.

```
static float SquareRoot (float n){    // Newton's Method (Basic Calculus)
float test1, test2;                    // Xₙ₊₁ = Xₙ - f(Xₙ)/f'(Xₙ)  n = 1, 2, 3,
... 
test1 = n-(float).01 -                 // X₀ = Guess-Estimate
    ((n-(float).01)*(n-(float).01) - n)/(n*(n-(float).01));
test2 = test1 - ((test1*test1)-n)/((n)*test1);

while (test1 != test2){                // X₁ = X₀ - (X₀² - Number)/(Number*X₀)
    test1 = test2;                     // X₁ = X₀ - (X₀² - Number)/(Number*X₀)
    test2 = test1 -                    // X₂ = X₁ - (X₁² - Number)/(Number*X₁)
        (test1*test1 - n) /            // X4 = X₃ - (X₃² - Number)/(Number*X₃)
        ((n)*test1);                   // X₆ = X₅ - (X₅² - Number)/(Number*X₅)
}
return (test2);                        // until Xₙ = Xₙ₊₁
}
```

Again, we can also reconstruct the last program using the predefined function Math.Sqrt() (see Example 2.42).

### Example 2.42. User-defined versus predefined functions.

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            float number = 0, root = 0;

            Console.WriteLine("This program will find the "
                + "square root of any number\n"
                + "To continue just enter a number when prompted\n"
                + "Your results will appear after you press enter\n"
                + "To quit just enter the number \"1\"^n"
                + "Enter your first value now: ");
            input = Console.ReadLine();
            number = float.Parse(input);
```

```csharp
class Class1 {
    static void Main() {
        string input = "Y", Horse;
        int iNumber1 = 0, iNumber2 = 0, iNumber3 = 0;

        Console.WriteLine("Let's have a horse race.\n"
            + "To play select one of the horses below");

        while (char.ToUpper(char.Parse(input)) != 'N') {
            Console.WriteLine("(1) for Whitefire\n"
                + "(2) for The Train and, \n"
                + "(3) for Noisy Glue\n");
            Horse = Console.ReadLine();

            TheRace(ref iNumber1);
            TheRace(ref iNumber2);
            TheRace(ref iNumber3);

            TieBreaker(iNumber1, ref iNumber2);
            TieBreaker(iNumber2, ref iNumber3);
            TieBreaker(iNumber1, ref iNumber3);

            Console.Write("And the winner is ");
            if (iNumber1 > iNumber2 && iNumber1 > iNumber3)
                Console.WriteLine("Noisy Glue"); // 3
            else if (iNumber2 > iNumber1 && iNumber2 > iNumber3)
                Console.WriteLine("The Train"); // 2
            else
                Console.WriteLine("Whitefire"); // 1

            Console.WriteLine("Would you like to play again (Y/N)?");
            input = Console.ReadLine();
        }
    }

    static void TheRace(ref int Num) {
        Random rnd = new Random();

        Num = (int)Math.Round(rnd.NextDouble() * 1000);
    }

    static void TieBreaker(int Num1, ref int Num2) {
        if (Num1 == Num2) {
TheRace(ref Num2);
TieBreaker(Num1, ref Num2);
} 
} 
}
```

## The Keyword out

The keyword out is a special exception marker that notifies the compiler that the variable under scrutiny does not need to be assigned before it can be passed as a referenced variable. This is usually the case when dealing with variables that wouldn't otherwise have a meaningful value before the appropriate functions can be executed. Since an out value is also a referenced value, this keyword negates the need for the second reference (ref) (see Example 2.44).

### Example 2.44. The keyword out.

```
using System;

namespace Chapter7 {
    class Class1 {
        static void Main() {
            string input = "Y", Horse;
            int iNumber1, iNumber2, iNumber3;

            Console.WriteLine("Let's have a horse race.\n"
                + "To play select one of the horses below");

            while (char.ToUpper(char.Parse(input)) != 'N') {
                Console.WriteLine("(1) for Whitefire\n"
                    + "(2) for The Train and, \n"
                    + "(3) for Noisy Glue\n");
                Horse = Console.ReadLine();

                TheRace (out iNumber1);
                TheRace (out iNumber2);
                TheRace (out iNumber3);

                TieBreaker (iNumber1, ref iNumber2);
                TieBreaker (iNumber2, ref iNumber3);
                TieBreaker (iNumber1, ref iNumber3);
Console.Write ("And the winner is");

if (iNumber1 > iNumber2 && iNumber1 > iNumber3)
    Console.WriteLine("Noisy Glue"); // 3
else if (iNumber2 > iNumber1 && iNumber2 > iNumber3)
    Console.WriteLine("The Train"); // 2
else
    Console.WriteLine("Whitefire"); // 1

Console.WriteLine("Would you like to play again (Y/N)?");
input = Console.ReadLine(); }

static void TheRace(out int Num) {
Random rnd = new Random();
Num = (int)Math.Round(rnd.NextDouble() * 1000);
}

static void TieBreaker(int Num1, ref int Num2) {
if (Num1 == Num2) {
    TheRace(out Num2);
    TieBreaker(Num1, ref Num2);
}
}
}
```

## An Introduction to Polymorphism

Polymorphism (also known as overloading) occurs when any reference has a closely matching, but not identical definition. These secondary, or substitute functions, while not technically required, generally tend to stay within the confines of the first function's purpose. If an overloading function were to be altered to a degree that promoted a completely new definition, then overloading would not be necessary. While overloading functions do share the same referencing title, their definitions must differ in arrangement by at least one transferring data type. The use of these differing access points guides the compiler to the correct (overloading) function. Since more than one possible referencing point exists, there is also an increased chance of miscalling that function, thus creating a runtime error. Examples 2.45 and 2.46 give alternate functions that can produce the same results, but only one is actually performing correctly.
