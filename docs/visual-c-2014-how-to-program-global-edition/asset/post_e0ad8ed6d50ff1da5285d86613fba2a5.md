
# Chapter 7 Methods: A Deeper Look

complete description of the class. Click the Methods link in the left-hand column to see a listing of the class's methods.

> Good Programming Practice 7.1
The online .NET Framework documentation is easy to search and provides many details about each class. As you learn each class in this book, you should review the class in the online documentation for additional information.

## 7.8 Case Study: Random-Number Generation

In this and the next section, we develop a nicely structured game-playing app with multiple methods. The app uses most of the control statements presented far in the book and introduces several new programming concepts.

There's something in the air of a casino that invites people—from the high rows at the plush mahogany-felt tables to the quarter near the one-armed bandits. It's the element of chance, the possibility that luck will convert a pocket of money into a mountain of wealth. The element of chance can be introduced in an app via an object of class Random (of Namespace System). Random can produce byte, int and double values. In the next examples, we use objects of class Random to produce random numbers.

## Secure Random Numbers

According to Microsoft's documentation for class Random, the random values it produces are not completely random because a mathematical algorithm is used to select them, but they are sufficiently random for practical purposes. Such values should not be used, for example, to randomly select selected passwords. If your app requires so-cryptographically secure random numbers, use RNGryptoServiceProvider to produce random values:

```
https://msdn.microsoft.com/library/system.security.cryptography.rngryptoserviceprovider
```

### 7.8.1 Creating an Object of Type Random

A new random-number generator object can be created with class Random (from the System namespace) as follows:

```
Random randomNumbers = new Random();
```

The Random object can then be used to generate random byte, int and double values—we discuss only int values here.

### 7.8.2 Generating a Random Integer

Consider the following statement:

```
int randomValue = randomNumbers.Next();
```

- 1. Class RNGryptoServiceProvider produces arrays of bytes. We discuss arrays in Chapter 8.

When called with no arguments, Next of class Random generates a random int in the range 0 to +2,147,483,646, inclusive. If the Next method produces values at random, every value in that range should have an equal chance (probability) of being chosen each time Next is called. The values returned by Next are actually pseudandom numbers—a sequence of values produced by a complex mathematical calculation. The calculation uses the current time of day (of course, changes constantly) to seed the random-number generator so that each execution of an app yields a different sequence of random values.

### 7.8.3 Scaling the Random-Number Range

The range of values produced by method Next often differs from the range of values required in a particular app. For example, an app that simulates coin tossing might require only 0 for "heads" and 1 for "tails." An app that rolls a six-sided die might require integers in the range 1–6. A video game that randomly predicts the next type of spacing (out of four possibilities) will fly across the horizon might require integers in the range 1–4. For cases like these, class Random provides versions of Next that accept arguments. It receives an int argument and returns a value from 0 up to, but not including, the argument's value. For example, you might use the statement

```
int randomValue = randomNumber.Next(6); // 0, 1, 2, 3, 4 or 5
```

returns 0, 1, 2, 3, 4 or 5. The argument—the scaling factor—represents the number of unique values that Next should produce (in this case, six—0, 1, 2, 3, 4 and 5). This manipulation is called scaling the values produced by Random method Next.

### 7.8.4 Shifting the Random-Number Range

Suppose we simulated a six-sided die that has the numbers 1–6 on its faces, not 0–5. The range of values alone is not enough. So we shift the numbers produced by shifting a value—in this case 1—to the result of method Next, as in

```
int face = 1 + randomNumber.Next(6); // 1, 2, 3, 4, 5 or 6
```

The shifting (1) specifies the first value in the desired set of random integers. The preceding statement assigns to face a random integer in the range 1–6.

### 7.8.5 Combining Shifting and Scaling

The third alternative method Next provides a more intuitive way to express both shifting and scaling. This method receives two int arguments and returns a value from the first argument's value up to, but not including, the second argument's value. We could use this method to write a statement equivalent to our previous statement, as in

```
int face = randomNumber.Next(1, 7); // 1, 2, 3, 4, 5 or 6
```

### 7.8.6 Rolling a Six-Sided Die

To demonstrate random numbers, let's develop an app that simulates 20 rolls of a six-sided die and displays each roll's value. Figure 7.6 shows two sample outputs, which confirm that the numbers produced by Next in the range 1–6 appear approximately equal. To show that equal likelihood, let's simulate 20 rolls of a six-sided die and display each roll's value.

```csharp
// RandomDie.cs
using System;

class RandomDie
{
    static void Main()
    {
        Random randomNumbers = new Random();
        int frequency1 = 0;
        int frequency2 = 0;
        int frequency3 = 0;
        int frequency4 = 0;
        int frequency5 = 0;
        int frequency6 = 0;

        for (int counter = 1; counter <= 20; counter++)
        {
            int face = randomNumbers.Next(1, 7); // number from 1 to 6
            Console.WriteLine($"{counter}: {face}"); // display the roll value
            switch (face)
            {
                case 1:
                    ++frequency1; // increment the 1s counter
                    break;
                case 2:
                    ++frequency2; // increment the 2s counter
                    break;
                case 3:
                    ++frequency3; // increment the 3s counter
                    break;
                case 4:
                    ++frequency4; // increment the 4s counter
                    break;
                case 5:
                    ++frequency5; // increment the 5s counter
                    break;
                case 6:
                    ++frequency6; // increment the 6s counter
                    break;
            }
        }

        Console.WriteLine("Face\tFrequency");
        Console.WriteLine($"1\t{frequency1}");
        Console.WriteLine($"2\t{frequency2}");
        Console.WriteLine($"3\t{frequency3}");
        Console.WriteLine($"4\t{frequency4}");
        Console.WriteLine($"5\t{frequency5}");
        Console.WriteLine($"6\t{frequency6}");
    }
}
```
