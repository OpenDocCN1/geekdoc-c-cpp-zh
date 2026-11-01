
// Counter
// Demonstrates for loops

#include <iostream>

using namespace std;

int main()
{
    cout << "Counting forward:\n";
    for (int i = 0; i < 10; ++i)
    {
        cout << i << " ";
    }

    cout << "\n\nCounting backward:\n";
    for (int i = 9; i >= 0; --i)
    {
        cout << i << " ";
    }

    cout << "\n\nCounting by fives:\n";
    for (int i = 0; i <= 50; i += 5)
    {
        cout << i << " ";
    }

    cout << "\n\nCounting with null statements:\n";
    int count = 0;
    for ( ; count < 10; )
    {
        cout << count << " ";
        ++count;
    }

    cout << "\n\nCounting with nested for loops:\n";
    const int ROWS = 5;
    const int COLUMNS = 3;
    for (int i = 0; i < ROWS; ++i)
    {
        for (int j = 0; j < COLUMNS; ++j)
        {
            cout << i << "," << j << " ";
        }

        cout << endl;
    }

    return 0;
}

## Trap

If you're using an older compiler that doesn't fully implement the current C++ standard, when you try to compile this program, you might get an error that says something like: error: 'i' : redefinition; multiple initialization.

The best solution is to use a modern, compliant compiler. Luckily, you can download the popular (and free) Microsoft Visual C++ Express Edition IDE, which includes a modern compiler, from http://www.microsoft.com/express/.

If you must use your old compiler, you should declare any for loop counter variables just once for all for loops in a scope. I cover the topic of scopes in Chapter 5, "Functions: Mad Lib."

## Counting with for Loops

The first for loop counts from 0 to 9. The loop begins:

```
for (int i = 0; i < 10; ++i)
```

The initialization statement, int i = 0, declares i and initializes it to 0. The expression i < 10 says that the loop will continue as long as i is less than 10. Lastly, the action statement, ++i, says i is to be incremented each time the loop body finishes. As a result, the loop iterates 10 times—once for each of the values 0 through 9. And during each iteration, the loop body displays the value of i.

The next for loop counts from 9 down to 0. The loop begins:

```
for (int i = 9; i >= 0; --i)
```

Here, i is initialized to 9, and the loop continues as long as i is greater than or equal to 0. Each time the loop body finishes, i is decremented. As a result, the loop displays the values 9 through 0.

The next loop counts from 0 to 50, by fives. The loop begins:

```
for (int i = 0; i <= 50; i += 5)
```

Here, i is initialized to 0, and the loop continues as long as i is less than or equal to 50. But notice the action statement, i += 5. This statement increases i by five each time the loop body finishes. As a result, the loop displays the values 0, 5, 10, 15, and so on. The expression i <= 50 says to execute the loop body as long as i is less than or equal to 50.

You can initialize a counter variable, create a test condition, and update the counter variable with any values you want. However, the most common thing to do is to start the counter at 0 and increment it by 1 after each loop iteration.

Finally, the caveats regarding infinite loops that you learned about while studying while loops apply equally well to for loops. Make sure you create loops that can end; otherwise, you'll have a very unhappy gamer on your hands.

## Using Empty Statements in for Loops

You can use empty statements in creating your for loop, as I did in the following loop:

```
for ( ; count < 10; )
```

I used an empty statement for the initialization and action statements. That's fine because I declared and initialized count before the loop and incremented it inside the loop body. This loop displays the same sequence of integers as the very first loop in the program. Although the loop might look odd, it's perfectly legal.

## Hint

> Different game programmers have different traditions. In the last chapter, you saw that you can create a loop that continues until it reaches an exit statement—such as a break—using while (true). Well, some programmers prefer to create these kinds of loops using a for statement that begins for (;;). Because the test expression in this loop is the empty statement, the loop will continue until it encounters some exit statement.

## Nesting for Loops

You can nest for loops by putting one inside the other. That's what I did in the following section of code, which counts out the elements of a grid. The outer loop, which begins:

```
for (int i = 0; i < ROWS; ++i)
```

simply executes its loop body ROWS (five) times. But it just so happens that there's another for loop inside this loop, which begins:

```
for (int j = 0; j < COLUMNS; ++j)
```

As a result, the inner loop executes in full for each iteration of the outer loop. In this case, that means the inner loop executes COLUMNS (three) times, for the ROWS (five) times the outer loop iterates, for a total of 15 times. Specifically, here's what happens:

- 1. The outer for loop declares i and initializes it to 0. Since i is less than ROWS (5), the program enters the outer loop's body.
- 2. The inner loop declares j and initializes it to 0. Since j is less than COLUMNS (3), the program enters its loop body, sending the values of i and j to cout, which displays 0, 0.
- 3. The program reaches the end of the body of the inner loop and increments j to 1. Since j is still less than COLUMNS (3), the program executes the inner loop's body again, displaying 0, 1.
- 4. The program reaches the end of the inner loop's body and increments j to 2. Since j is still less than COLUMNS (3), the program executes the inner loop's body again, displaying 0, 2.
- 5. The program reaches the end of the inner loop's body and increments j to 3. This time, however, j is not less than COLUMNS (3) and the inner loop ends.
- 6. The program finishes the first iteration of the outer loop by sending endl to cout, ending the first row.
- 7. The program reaches the end of the outer loop's body and increments i to 1. Since i is less than ROWS (5), the program enters the outer loop's body again.

![](img/c7e8651578bccd573227f684823b8754_110_0.png)

## Figure 3.2

This representation of the definition of an alien spacecraft says that each object will have a data member called energy and a member function called fireWeapons().

The cool thing about objects is that you don’t need to know the implementation details to use them—just as you don’t need to know how to build a car in order to drive one. You only have to know the object’s data members and member functions—just as you only have to know where a car’s steering wheel, gas pedal, and brake pedal are located.

You can store objects in variables, just like with built-in types. Therefore, you could store an alien spacecraft object in a variable of the Spacecraft type. You can access data members and member functions using the member selection operator (.), by placing the operator after the variable name of the object. So if you want your alien spacecraft, ship, to fire its weapons only if its energy level is greater than 10, you could write:

```
// ship is an object of Spacecraft type
if (ship.energy > 10)
{
    ship.fireWeapons()
}
```

ship.energy accesses the object's energy data member, while ship.fireWeapons() calls the object's fireWeapons() member function.

Although you can't make your own new types (like for an alien spacecraft) just yet, you can work with previously defined object types. And that's next on the agenda.

## USING STRING OBJECTS

string objects, which you met briefly in Chapter 1, are the perfect way to work with sequences of characters, whether you're writing a complete word puzzle game or simply storing a player's name. A string is actually an object, and it provides its own set of member functions that allow you to do a range of things with the string object—everything from simply getting its length to performing complex character substitutions. In addition, strings are defined so that they work intuitively with a few of the operators you already know.

## Introducing the String Tester Program

The String Tester program uses the string object equal to "Game Over!!!" and tells you its length, the index (position number) of each character, and whether or not certain substrings can be found in it. In addition, the program erases parts of the string object. Figure 3.3 shows the results of the program.

![](img/c7e8651578bccd573227f684823b8754_111_0.png)

Figure 3.3
String objects are combined, changed, and erased through familiar operators and string member functions.
