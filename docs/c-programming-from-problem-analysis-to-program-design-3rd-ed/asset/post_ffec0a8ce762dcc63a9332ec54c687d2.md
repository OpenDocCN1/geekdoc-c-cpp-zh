
With call by reference, no copy is made of the contents. A copy is made of the reference (address) to the location in which the array is stored, and the copy is stored in a variable. As shown in Figure 7-7, the formal parameter, temp, references the same location in memory as temperature does. The values entered into the temp array in the InputValues( ) method are stored in the memory cells referenced by temperature.

## Array Assignment

The assignment operator = may not work as you would think it should when used with reference types such as arrays. If an additional array is defined and an assignment is made, the assignment operator and the array reference the same elements. Individual elements are not copied to another memory location. Consider the following statements that could be written after the temperature array is filled with values:

```csharp
int [ ] t = new int[5];
t = temperature;
t[1] = 44;
```

Figure 7-8 illustrates the result of the assignment statements. Any reference to temperature[1] accesses 44.

![](img/e33ae760e23d89eac66541252ad65de8_414_0.png)

Figure 7-8 Assignment of an array to reference another array

Example 7-13 includes the complete code listing from the program statements used in Figures 7-7 and 7-8, which illustrate the assignment and use of arrays as method parameters.

### Example 7-13

```csharp
/* PassingArray.cs    Author: Doyle
 * Demonstrates passing
 * arrays to methods - references
 */
using System;
namespace PassingArray
{
    class PassingArray
    {
        static void Main( )
        {
            int [ ] temperature = new int[5];
            int [ ] t = new int[5];

            InputValues(temperature);

            //Array t will reference the same array
            //as the temperature array.
            t = temperature;
            t[1] = 44;
            Console.WriteLine(temperature[1]);
        }

        public static void InputValues(int [ ] temp)
        {
            string inValue;

            for(int i = 0; i < temp.Length; i++)
            {
                Console.Write("Enter Temperature {0}: ", i + 1);
                inValue = Console.ReadLine( );
                temp[i] = int.Parse(inValue);
            }
        }
    }
}
```

## Params Parameters

In Chapter 3, you were briefly introduced to the params parameter type. When a method uses the params modifier, the parameter is considered a parameter array. It is used to indicate that the number of arguments to the method may vary.

![](img/e33ae760e23d89eac66541252ad65de8_416_0.png)

If you include the params argument in the method heading, the array identifier it is used with must be the last parameter listed in the method heading. The identifier cannot be defined as a ref or out parameter.

The keyword params appears only in the formal parameter list of the method heading. By including it, the method may be called one time with a single value. Another call to the same method could send 10 or 100 values or an array of values. A variable number of arguments are accepted when params is included. It makes the method very flexible. Example 7-14 shows how a method defined with a parameter array can be called with both simple value arguments and with an array.

### Example 7-14

```csharp
/* VaryingArguments.cs    Author: Doyle
 * This example demonstrates the use
 * of the params keyword. A varying
 * number of arguments can be sent
 * to a method.
 */
using System;
namespace VaryingArguments
{
    class VaryingArguments
    {
        public static void Main( )
        {
            DisplayItems(1, 2, 3, 5);
            int[] anArray = new int[5] {100, 200,
                                        300, 400, 500};
            DisplayItems(anArray);
            DisplayItems(1500, anArray[1] * anArray[2]);
        }
        public static void DisplayItems(params int[] item)
        {
            for ( int i = 0; i < item.Length; i++ )
            {
                Console.Write(item[i] + "\t");
            }
            Console.WriteLine( );
        }
    }
}
```

The first call to the `DisplayItems()` method includes four arguments (1, 2, 3, 5). They match the `DisplayItems()` heading of `(params int[] item)`. The second call sends an array as an argument during the method call. The last call sends two arguments; the first is 1500, a constant literal. The second argument for the last call is an expression that involves multiplying 200 times 300 (`anArray[1] * anArray[2]`). This result is an integer; thus, all are acceptable arguments when the `params` keyword is included in the parameter list. The output produced is as follows:

```
1       2       3       5
100     200     300     400     500
1500    60000
```

## ARRAYS IN CLASSES

Arrays can be used as fields or instance variables in classes. Normally, the base type is declared with the other instance variables. But, space is allocated when an object of that class is instantiated. Consider the following list of data members of the Player class. In addition to the descriptive characteristics about a player, an array for pointsScored is defined. For instance, the player might score 10 points in the first game, 0 in the second, and so on.

```csharp
public class Player
{
    private string lname;
    private string fname;
    private string id;
    private int[] pointsScored;
    private int numberOfGames;
    private double avg;
}
```

After the Player class is defined, any number of games and associated points scored per game could be used to instantiate an object of the class. As you think about the characteristics of a player, you realize that you cannot say that all team players play 50 games or 5 games; thus, no space is allocated in the pointsScored array for a certain number of games. Because this is an instance member, allocate space when you construct an object of the class. This enables the class to be more flexible and usable by a larger number of applications.

Because one player might have played in 50 games and another player only 37, you need to know how many different games to record scores. The pointsScored[] array is used to hold the player's scores for each game. In addition to the default constructor, a constructor is defined that receives multiple arguments including the number of games a player played. This is sent in as an argument from the application through the numGames variable. Thus, if numGames has a value of 10, the first 10 elements of the pointsScored[] array would hold game counts (one per game). The constructor contains parameters for all instance variables, except the average. This is a calculated value.

The heading for the constructor follows:

```csharp
public Player (string ln, string fn, string iden,
               int [ ] s, int numGames)
```

> You might think you could just use the value of `s.Length` to determine the number of games instead of sending in the number of games argument. Remember that `Length` returns the total number of dimensioned elements, even those that are unused. The `Length` value does not represent how many elements are nonzero.

Space is allocated for the **pointsScored** array using the **numGames** argument. The following **Player** member method is used:

```csharp
public void FillPointsScoredArray(int [ ] s)
{
        pointsScored = new int [numberOfGames];
        for (int i = 0; i < pointsScored.Length; i++)
            pointsScored[i] = s[i];
}
```

Before the preceding method can be called, an **object** of the **Player class** has to be constructed. A value would already be associated with the field member **numberOfGames**. The first statement in the body of the `FillPointsScoredArray( )` method instantiates the **array object** by allocating space for the number of elements using that instance field member. The last statement then copies the elements from the array **s**, which was sent into the method, to the instance array member, **pointsScored**.

The length of **s** could not be used as a loop control variable because it does not accurately indicate how many actual values are sent into the method. **Length** is the number of dimensioned elements, which was 1000 in the application using the **Player class**. Remember, one of the goals of creating classes is to be able to reuse the **class** with different applications. The current **Player class** determines the average points scored by a player. Additional methods could be written to return the number of games played, the high and low scores, the number of games in which the player scored at least 10 points, and so on. A parallel array could be created to associate **pointsScored** with the opponent name.

**Parallel arrays** are two or more arrays that have a relationship. The relationship is established using the same subscript or index to refer to the elements. For example, opponent X's name might be stored in a **string** array at index location C. Then, the number of points the player made against opponent X would be stored at that same indexed location C in another array. Parallel arrays are especially useful for storing related data when the related data is of different types.

> With parallel arrays, `anArrayOne[0]` is related to `anArrayTwo[0]`, `anArrayOne[1]` is related to `anArrayTwo[1]`, `anArrayOne[2]` is related to `anArrayTwo[2]`, and so on.
