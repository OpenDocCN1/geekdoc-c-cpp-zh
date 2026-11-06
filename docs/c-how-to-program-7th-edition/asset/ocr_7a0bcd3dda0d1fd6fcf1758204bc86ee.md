wager, print the new bankBalance, check on whether bankBalance has become zero and, if so, print the message "Sorry. You busted!" As the game progresses, print various messages to create some "chatter" such as "Oh, you're going for broke, huh?", "Aw c'mon, take a chance!" or "You're up big. Now's the time to cash in your chips!".

**6.50 (Circle Area)** Write a C++ program that prompts the user for the radius of a circle, then calls inline function circleArea to calculate the area of that circle.

**6.51 (Pass-by-Value vs. Pass-by-Reference)** Write a complete C++ program with the two alternate functions specified below, each of which simply triples the variable count defined in main. Then compare and contrast the two approaches. These two functions are

+   a) function tripleByValue that passes a copy of count by value, triples the copy and returns the new value and
+   
+   b) function tripleByReference that passes count by reference via a reference parameter and triples the original value of count through its alias (i.e., the reference parameter).

**6.52** What's the purpose of the unary scope resolution operator?

**6.53 (Function Template minimum)** Write a program that uses a function template called minimum to determine the smaller of two arguments. Test the program using integer, character and floating-point number arguments.

**6.54 (Function Template maximum)** Write a program that uses a function template called maximum to determine the larger of two arguments. Test the program using integer, character and floating-point number arguments.

**6.55 (Find the Error)** Determine whether the following program segments contain errors. For each error, explain how it can be corrected. [Note: For a particular program segment, it's possible that no errors are present in the segment.]

```
a)
    template < class A >
    int sum( int num1, int num2, int num3 )
    {
        return num1 + num2 + num3;
    }
```

```
b)
    void printResults( int x, int y )
    {
        cout << "The sum is " << x + y << '\n';
        return x + y;
    }
```

```
c)
    template < A >
    A product( A num1, A num2, A num3 )
    {
        return num1 * num2 * num3;
    }
```

```
d)
    double cube( int );
    int cube( int );
```

# Making a Difference

As computer costs decline, it becomes feasible for every student, regardless of economic circumstance, to have a computer and use it in school. This creates exciting possibilities for improving the educational experience of all students worldwide as suggested by the next five exercises. [Note: Check out initiatives such as the One Laptop Per Child Project (www.laptop.org). Also, research "green" laptops—and note the key "going green" characteristics of these devices? Look into the