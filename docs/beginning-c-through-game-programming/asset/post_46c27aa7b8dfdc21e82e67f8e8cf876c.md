
```cpp
// Pointing
// Demonstrates using pointers

#include <iostream>
#include <string>

using namespace std;

int main()
{
    int* pAPointer;     // declare a pointer

    int* pScore = 0;    // declare and initialize a pointer

    int score = 1000;
    pScore = &score;    // assign pointer pScore address of variable score

    cout << "Assigning &score to pScore\n";
    cout << "&score is: " << &score << "\n";    // address of score variable
    cout << "pScore is: " << pScore << "\n";    // address stored in pointer
    cout << "score is: " << score << "\n";
    cout << "*pScore is: " << *pScore << "\n\n"; // value pointed to by pointer

    cout << "Adding 500 to score\n";
    score += 500;
    cout << "score is: " << score << "\n";
    cout << "*pScore is: " << *pScore << "\n\n";

    cout << "Adding 500 to *pScore\n";
    *pScore += 500;
    cout << "score is: " << score << "\n";
    cout << "*pScore is: " << *pScore << "\n\n";

    cout << "Assigning &newScore to pScore\n";
    int newScore = 5000;
    pScore = &newScore;
    cout << "&newScore is: " << &newScore << "\n";
    cout << "pScore is: " << pScore << "\n";
    cout << "newScore is: " << newScore << "\n";
    cout << "*pScore is: " << *pScore << "\n\n";

    cout << "Assigning &str to pStr\n";
    string str = "score";
    string* pStr = &str;  // pointer to string object
    cout << "str is: " << str << "\n";
    cout << "*pStr is: " << *pStr << "\n";
    cout << "(*pStr).size() is: " << (*pStr).size() << "\n";
    cout << "pStr->size() is: " << pStr->size() << "\n";

    return 0;
}
```

## Declaring Pointers

With the first statement in main() I declare a pointer named pAPointer.

```cpp
int* pAPointer;    // declare a pointer
```

Because pointers work in such a unique way, programmers often prefix pointer variable names with the letter "p" to remind them that the variable is indeed a pointer.

Just like an iterator, a pointer is declared to point to a specific type of value. pAPointer is a pointer to int, which means that it can only point to an int value. pAPointer can't point to a float or a char, for example. Another way to say this is that pAPointer can only store the address of an int.

To declare a pointer of your own, begin with the type of object to which the pointer will point, followed by an asterisk, followed by the pointer name. When you declare a pointer, you can put whitespace on either side of the asterisk. So `int* pAPointer;`, `int *pAPointer;`, and `int * pAPointer;` all declare a pointer named pAPointer.

### Trap

When you declare a pointer, the asterisk only applies to the single variable name that immediately follows it. So the following statement declares pScore as a pointer to int and score as an int.

```cpp
int* pScore, score;
```

score is not a pointer! It's a variable of type int. One way to make this clearer is to play with the whitespace and rewrite the statement as:

```cpp
int *pScore, score;
```

![Figure 7.2](img/c7e8651578bccd573227f684823b8754_250_0.png)

Figure 7.2 — The pointer pScore points to score, which stores the value 1000.

To prove that pScore contains the address of score, I display the address of the variable and the value of the pointer with the following lines.

```cpp
cout << "&score is: " << &score << "\n";    // address of score variable
cout << "pScore is: " << pScore << "\n";    // address stored in pointer
```

pScore contains 0x22ff5c, which is the address of score. (The specific addresses displayed by the Pointing program might be different on your system. The important thing is that the values for pScore and &score are the same.)

## Dereferencing Pointers

Just as you dereference an iterator to access the object to which it refers, you dereference a pointer to access the object to which it points. You accomplish the dereferencing the same way—with *, the dereference operator. I put the dereference operator to work with the following line, which displays 1000 because *pScore accesses the value stored in score.

```cpp
cout << "*pScore is: " << *pScore << "\n"; // value pointed to by pointer
```

Remember, *pScore means, "the object to which pScore points."

### Trap

> Don't dereference a null pointer because it could lead to disastrous results.

Next, I add 500 to score with the following line.

```cpp
score += 500;
```

When I send score to cout, 1500 is displayed, as you'd expect. When I send *pScore to cout, the contents of score are again sent to cout, and 1500 is displayed once more.

Next, I add 500 to the value to which pScore points with the following line.

```cpp
*pScore += 500;
```

Because pScore points to score, the preceding line of code adds 500 to score. Therefore, when I next send score to cout, 2000 is displayed. Then, when I send *pScore to cout...you guessed it, 2000 is displayed again.

### Trap

Don't change the value of a pointer when you want to change the value of the object to which the pointer points. For example, if I want to add 500 to the int that pScore points to, then the following line would be a big mistake.

```cpp
pScore += 500;
```

The preceding code adds 500 to the address stored in pScore, not to the value to which pScore originally pointed. As a result, pScore now points to some address that might contain anything. Dereferencing a pointer like this can lead to disastrous results.

## Reassigning Pointers

Unlike references, pointers can point to different objects at different times during the life of a program. Reassigning a pointer works like reassigning any other variable. Next, I reassign pScore with the following line.

```cpp
pScore = &newScore;
```

As a result, pScore now points to newScore. To prove this, I display the address of newScore by sending &newScore to cout, followed by the address stored in pScore. Both statements display the same address. Then I send newScore and *pScore to cout. Both display 5000 because they both access the same chunk of memory that stores this value.

### Trap

Don't change the value to which a pointer points when you want to change the pointer itself. For example, if I want to change pScore to point to newScore, then the following line would be a big mistake.

```cpp
*pScore = newScore;
```

This code simply changes the value to which pScore currently points; it doesn't change pScore itself. If newScore is equal to 5000, then the previous code is equivalent to *pScore = 5000; and pScore still points to the same variable it pointed to before the assignment.

## Using Pointers to Objects

So far, the Pointing program has worked only with values of a built-in type, int. But you can use pointers with objects just as easily. I demonstrate this next with the following lines, which create str, a string object equal to "score", and pStr, a pointer that points to that object.

```cpp
string str = "score";
string* pStr = &str;  // pointer to string object
```

pStr is a pointer to string, meaning that it can point to any string object. Another way to say this is to say that pStr can store the address of any string object.

You can access an object through a pointer using the dereference operator. That's what I do next with the following line.

```cpp
cout << "*pStr is: " << *pStr << "\n";
```

By using the dereference operator with *pStr, I send the object to which pStr points (str) to cout. As a result, the text score is displayed.

You can call the member functions of an object through a pointer the same way you can call the member functions of an object through an iterator. One way to do this is by using the dereference operator and the member access operator, which is what I do next with the following lines.

```cpp
cout << "(*pStr).size() is: " << (*pStr).size() << "\n";
```

The code `(*pStr).size()` says, "Take the result of dereferencing pStr and call that object's size() member function." Because pStr refers to the string object equal to "score", the code returns 5.

> **Hint**
>
> Whenever you dereference a pointer to access a data member or member function, surround the dereferenced pointer with a pair of parentheses. This ensures that the dot operator will be applied to the object to which the pointer points.

Just as with iterators, you can use the -> operator with pointers for a more readable way to access object members. That's what I demonstrate next with the following line.

```cpp
cout << "pStr->size() is: " << pStr->size() << "\n";
```
