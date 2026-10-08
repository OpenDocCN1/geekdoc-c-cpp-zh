
# Chapter 8 Arrays: Introduction to Exception Handling

## Class DeckOfCards: DealCard Method
Method DealCard (lines 48–59) deals the next card in the array. Recall that currentCard index of the next Card to be dealt (i.e., the Card at the top of the deck). Thus, line 51 compares currentCard to the length of the deck array. If the deck is not empty (i.e., currentCard is less than 52), line 53 returns the top Card and increments currentCard for the next call to DealCard—otherwise, line 57 returns null to indicate the end of deck has been reached.

## 8.6.3 Shuffling and Dealing Cards
Figure 8.12 demonstrates the shuffling and dealing capabilities of class DeckOfCards (Fig. 8.11). Line 10 of Fig.12 creates a DeckOfCards object named myDeckCards and use type inference to determine the variable's type. Recall that the DeckOfCards constructor initializes the deck with the 52 Cards in order by suit and face. Line 11 invokes myDeckCards's Shuffle method to rearrange the Card objects. For the statement in lines 14-22 deals all 52 Cards in the deck and displays them in four columns of 13 Cards Each line and displays a Card object by invoking myDeckCards's DealCard Method. When a card object is placed in a string-interpolation expression, the Card’s ToString method is invoked. Because the field width is negative, the result is displayed left-aligned in a field width of 19.

```c
// Fig.8.12: DeckOfCardsTest.cs
// Card shuffling and dealing app.
using System;
class DeckOfCardsTest
{
    // execute app
    static void Main()
    {
        var myDeckCards = new DeckOfCards();
        myDeckCards.Shuffle(); // place Cards in random order

        // display all 52 Cards in the order in which they are dealt
        for (var i = 0; i < 52; i++)
        {
            Console.Write($"{myDeckCards.DealCard(i), -19}");

            if ((i + 1) % 4 == 0)
            {
                Console.WriteLine();
            }
        }
    }
}
```

| Eight of Clubs | Ten of Clubs | Ten of Spades | Four of Spades |
| --- | --- | --- | --- |
| Ace of Spades | Jack of Spades | Three of Spades | Seven of Spades |
| Three of Diamonds | Five of Clubs | Eight of Spades | Five of Hearts |

Fig. 8.12 | Card-shuffling-and-dealing-app. (Part 1 of 2)

| Ace of Hearts | Ten of Hearts | Deuce Hearts | Deuce of Clubs |
| --- | --- | --- | --- |
| Jack of Hearts | Nine of Spades | Four of Hearts | Seven of Clubs |
| Queen of Spades | Seven of Diamonds | Five of Diamonds | Ace of Hearts |
| Four of Clubs | Ten of Diamonds | Jack of Clubs | Six of Diamonds |
| Eight of Diamonds | King of Hearts | Three of Clubs | King of Spades |
| King of Hearts | Six of Diamonds | Deuce of Spades | Five of Spades |
| Queen of Clubs | King of Clubs | Queen of Hearts | Seven of Hearts |
| Ace of Diamonds | Deuce of Hearts | Four of Diamonds | Nine of Clubs |
| Queen of Diamonds | Jack of Diamonds | Six of Hearts | Nine of Diamonds |
| Nine of Hearts | Three of Hearts | Six of Clubs | Eight of Hearts |

**Fig. 8.12** Card-shuffling-and-dealing.app (Part 2 of 2.)

## 8.7 Passing Arrays and Array Elements to Methods

To pass an argument to a method, specify the name of the array without any brackets. For example, if hourlyTemperatures is declared as

```c
var hourlyTemperatures = new double[24];
```

then the method call

```c
modifyArray(hourlyTemperatures);
```

passes the reference of array hourlyTemperatures to modifyArray. Every array object "knows" its own length (and makes it available via its Length property). Thus, when we pass an array object to a method, we do not pass the array length as an additional argument.

### Specifying an Array Parameter
For a method to receive an array reference through a method call, the method must list an array parameter. For example, the method header for method modifyArray might be written as

```csharp
void modifyArray(double[] b)
```

indicating that modifyArray receives the reference of an array of doubles in parameter b. The method passes array hourlyTemperatures reference, so when the method calls variable b, it refers to the same array object as hourlyTemperatures in the calling method.

### Pass-By-Value vs. Pass-By-Reference
When an argument is an entire array or an individual array element of reference type, the called method receives a copy of the reference. However, when an argument to a method is an individual array element of value type, the called method receives a copy of the element's value. To pass an individual array element to a method, use the indexed name of the array as an argument (e.g., hourlyTemperatures[2]). If you want to pass a value-type array to a method, you must use the ref keyword as shown in Section 7.18.

### Passing an Entire Array vs. Passing a Single Element
Figure 8.13 demonstrates the difference between passing an entire array and passing a value-type array element to a method. The foreach statement at lines 16–19 outputs the five elements of array. Line 21 invokes modifyArray, passing array as an argument. Method ModifyArray (lines 38–44) receives a copy of array reference and uses the reference to multiply each of array elements by 2. To prove that array's elements (in Main) were modified, the foreach statement at lines 25–28 outputs the five elements of array again. As the output shows, method ModifyArray doubled the value of each element.

```csharp
// Fig.13: PassArray.cs
// Passing arrays and individual array elements to methods.
using System;
class PassArray
{
    // Main create arrays and calls ModifyArray
    static void Main()
    {
        int[] array = {1, 2, 3, 4, 5};
        Console.WriteLine("Effects of passing reference to entire array:");
        Console.WriteLine("The values of the original array are:");
        
        // output original array elements
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }

        ModifyArray(array); // pass array reference
        Console.WriteLine("\nValues of the modified array are:");
        
        // output modified array elements
        foreach (var value in array)
        {
            Console.Write($"{value}");
        }

        Console.WriteLine("\nEffects of passing element value:\n" + $"{array[3]} before ModifyElement: {array[3]}");
        ModifyElement(array[3]); // attempt to modify array[3]
        Console.WriteLine($"{array[3]} after ModifyElement: {array[3]}");
    }

    // multiply each element of array by 2
    static void ModifyArray(int[] array2)
    {
        for (var counter = 0; counter < array2.Length; ++counter)
            array2[counter] *= 2;
    }
}
```
**Fig. 8.13** Passing arrays and individual array elements to methods. (Part I of 2.)

## 8.8 Case Study: GradeBook Using an Array to Store Grades

```csharp
// multiply argument by 2
static void ModifyElement(int element)
{
    element *= 2;
    Console.WriteLine($"Value of element in ModifyElement: {element}");
}
```

Effects of passing reference to entire array:
The values of the original array are:
1 2 3 4 5

The values of the modified array are:
2 4 6 8 10

Effects of passing element value:
array[3] before ModifyElement: 8
Value of element in ModifyElement: 16
array[3] after ModifyElement: 8

Fig. 8.13 | Passing arrays and individual array elements to methods. (Part 2 of 2.)

8.13 next demonstrates that when a copy of an individual value-type element is passed to a method, modifying the copy in the called method does not affect the original value of element in the callings method. To show the value of array[3] before invoking ModifyElement, lines 30–31 display the value of array[3], which is 8. Line 33 calls ModifyElement (lines 47–51) passes array[3] as an argument. Remember that array[3] is actually one int (8) in array. Therefore, the app passes a copy of the value of array[3]. Method ModifyElement multiplies the value received as an argument by 2, results then outputs the value of element (16). Since method parameters, like local variables, cease to exist when the method in which they are declared execution, the method parameter element is destroyed when ModifyElement terminates. When the app returns to Main, line 34 displays the unmodified value of array[3] (i.e., 8).

## 8.8 Case Study: GradeBook Using an Array to Store Grades
We now present the first version of a GradeBook that instructors can use to maintain students' grades on an exam and display a grade report that includes the grades, class average, lowest, highest grade and a grade distribution chart. The version of GradeBook presented in this section stores the grades for one exam in a one-dimensional array. In Section 8.10, we present a second version of GradeBook that uses a two-dimensional array to store students' grades for several exams.

### Storing Grades in an array in class GradeBook
Figure 8.14 shows how the output summarizes the 10 grades we store in an object of class GradeBook (Fig. 8.15), which uses an array of integers to store the grades of 10 students for a single exam. The array is declared as an instance variable in line 7 of Fig. 8.15—therefore, each GradeBook object maintains its own set of grades.
