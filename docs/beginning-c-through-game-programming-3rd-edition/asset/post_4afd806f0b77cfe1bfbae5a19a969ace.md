
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

## Nesting for Loops

You can nest for loops by putting one inside the other. That’s what I did in the following section of code, which counts out the elements of a grid. The outer loop, which begins:

```
for (int i = 0; i < ROWS; ++i)
```

simply executes its loop body ROWS (five) times. But it just so happens that there’s another for loop inside this loop, which begins:

```
for (int j = 0; j < COLUMNS; ++j)
```

As a result, the inner loop executes in full for each iteration of the outer loop. In this case, that means the inner loop executes COLUMNS (three) times, for the ROWS (five) times the outer loop iterates, for a total of 15 times. Specifically, here’s what happens:

- 1. The outer for loop declares i and initializes it to 0. Since i is less than ROWS (5), the program enters the outer loop’s body.
- 2. The inner loop declares j and initializes it to 0. Since j is less than COLUMNS (3), the program enters its loop body, sending the values of i and j to cout, which displays 0, 0.
- 3. The program reaches the end of the body of the inner loop and increments j to 1. Since j is still less than COLUMNS (3), the program executes the inner loop’s body again, displaying 0, 1.
- 4. The program reaches the end of the inner loop’s body and increments j to 2. Since j is still less than COLUMNS (3), the program executes the inner loop’s body again, displaying 0, 2.
- 5. The program reaches the end of the inner loop’s body and increments j to 3. This time, however, j is not less than COLUMNS (3) and the inner loop ends.
- 6. The program finishes the first iteration of the outer loop by sending endl to cout, ending the first row.
- 7. The program reaches the end of the outer loop’s body and increments i to 1. Since i is less than ROWS (5), the program enters the outer loop’s body again.

8. The program reaches the inner loop, which starts from the beginning once again, by declaring and initializing j to 0. The program goes through the process I described in Steps 2 through 7, displaying the second row of the grid. This process continues until all five rows have been displayed.

Again, the important thing to remember is that the inner loop is executed in full for each iteration of the outer loop.

## UNDERSTANDING OBJECTS

So far you’ve seen how to store individual pieces of information in variables and how to manipulate those variables using operators and functions. But most of the things you want to represent in games—such as, say, an alien spacecraft—are objects. They’re encapsulated, cohesive things that combine qualities (such as an energy level) and abilities (for example, firing weapons). Often it makes no sense to talk about the individual qualities and abilities in isolation from each other.

Fortunately, most modern programming languages let you work with software objects (often just called objects) that combine data and functions. A data element of an object is called a data member, while a function of an object is called a member function. As a concrete example, think about that alien spacecraft. An alien spacecraft object might be of a new type called Spacecraft, defined by a game programmer, and might have a data member for its energy level and a member function to fire its weapons. In practice, an object’s energy level might be stored in its data member energy as an int, and its ability to fire its weapons might be defined in a member function called fireWeapons().

Every object of the same type has the same basic structure, so each object will have the same set of data members and member functions. However, as an individual, each object will have its own values for its data members. If you had a squadron of five alien spacecrafts, each would have its own energy level. One might have an energy level of 75, while another might have a level of only 10, and so on. Even if two crafts have the same energy level, each would belong to a unique spacecraft. Each craft could also fire its own weapons with a call to its member function, fireWeapons(). Figure 3.2 illustrates the concept of an alien spacecraft.

![](img/34f09be0ed6217c465debc4490197d4f_110_0.png)

### Figure 3.2

This representation of the definition of an alien spacecraft says that each object will have a data member called energy and a member function called fireWeapons().

The cool thing about objects is that you don’t need to know the implementation details to use them—just as you don’t need to know how to build a car in order to drive one. You only have to know the object’s data members and member functions—just as you only need to know where a car’s steering wheel, gas pedal, and brake pedal are located.

You can store objects in variables, just like with built-in types. Therefore, you could store an alien spacecraft object in a variable of the Spacecraft type. You can access data members and member functions using the member selection operator (.), by placing the operator after the variable name of the object. So if you want your alien spacecraft, ship, to fire its weapons only if its energy level is greater than 10, you could write:

```
// ship is an object of Spacecraft type
if (ship.energy > 10)
{
    ship.fireWeapons()
}
```

## Indexing a string Object

A string object stores a sequence of char values. You can access any individual char value by providing an index number with the subscripting operator ([]). That’s what I do next:

```
cout << "The character at position 0 is: " << phrase[0] << "\n\n";
```

The first element in a sequence is at position 0. In the previous statement, phrase [0] is the character G. And because counting begins at 0, the last character in the string object is phrase[11], even though the string object has 12 characters in it.

### Trap

> It’s a common mistake to forget that indexing begins at position 0. Remember, a string object with n characters in it can be indexed from position 0 to position n − 1.

Not only can you access characters in a string object with the subscripting operator, but you can also reassign them. That’s what I do next:

```
phrase[0] = 'L';
```

I change the first character of phrase to the character L, which means phrase becomes "Lame Over!!!"

### Trap

> C++ compilers do not perform bounds checking when working with string objects and the subscripting operator. This means that the compiler doesn’t check to see whether you’re attempting to access an element that doesn’t exist. Accessing an invalid sequence element can lead to disastrous results because it’s possible to write over critical data in your computer’s memory. By doing this, you can crash your program, so take care when using the subscripting operator.

## Iterating through string Objects

Given your new knowledge of for loops and string objects, it’s a snap to iterate through the individual characters of a string object. That’s what I do next:

```
for (unsigned int i = 0; i < phrase.size(); ++i)
{
    cout << "Character at position " << i << " is: " << phrase[i] << endl;
}
```

The loop iterates through all of the valid positions of `phrase`. It starts with 0 and goes through 11. During each iteration, a character of the `string` object is displayed with `phrase[i]`. Note that I made the loop variable, `i`, an unsigned int because the value returned by `size()` is an unsigned integral type.

## Real World

Iterating through a sequence is a powerful and often-used technique in games. You might, for example, iterate through hundreds of individual units in a strategy game, updating their status and order. Or you might iterate through the list of vertices of a 3D model to apply some geometric transformation.

## Using the find() Member Function

Next I use the member function `find()` to check whether either of two string literals are contained in `phrase`. First, I check for the string literal "Over":

```
cout << "\nThe sequence 'Over' begins at location ";
cout << phrase.find("Over") << endl;
```

The `find()` member function searches the calling string object for the string supplied as an argument. The member function returns the position number of the first occurrence where the string object for which you are searching begins in the calling string object. This means that `phrase.find("Over")` returns the position number where the first occurrence of "Over" begins in `phrase`. Since `phrase` is "Lame Over!!!", `find()` returns 5. (Remember, position numbers begin at 0, so 5 means the sixth character.)

But what if the string for which you are searching doesn’t exist in the calling string? I tackle that situation next:

```
if (phrase.find("eggplant") == string::npos)
{
    cout << "'eggplant' is not in the phrase.\n\n";
}
```

Because "eggplant" does not exist in `phrase`, `find()` returns a special constant defined in the file `string`, which I access with `string::npos`. As a result, the screen displays the message, “'eggplant' is not in the phrase.”
