
The preceding statement again displays the number of characters in the string object equal to "score"; however, I'm able to substitute pStr->size() for (*pStr).size() this time, making the code more readable.

## UNDERSTANDING POINTERS AND CONSTANTS

There are still some pointer mechanics you need to understand before you can start to use pointers effectively in your game programs. You can use the keyword const to restrict the way a pointer works. These restrictions can act as safeguards and can make your programming intentions clearer. Since pointers are quite versatile, restricting how a pointer can be used is in line with the programming mantra of asking for only what you need.

## Using a Constant Pointer

As you've seen, pointers can point to different objects at different times in a program. However, by using the const keyword when you declare and initialize a pointer, you can restrict the pointer so it can only point to the object it was initialized to point to. A pointer like this is called a constant pointer. Another way to say this is to say that the address stored in a constant pointer can never change—it's constant. Here's an example of creating a constant pointer:

```c
int score = 100;
int* const pScore = &score;  // a constant pointer
```

The preceding code creates a constant pointer, pScore, which points to score. You create a constant pointer by putting const right before the name of the pointer when you declare it.

Like all constants, you must initialize a constant pointer when you first declare it. The following line is illegal and will produce a big, fat compile error.

```c
int* const pScore;  // illegal -- you must initialize a constant pointer
```

Because pScore is a constant pointer, it can't ever point to any other memory location. The following code is also quite illegal.

```c
pScore = &anotherScore;  // illegal - pScore can't point to a different object
```

Although you can't change pScore itself, you can use pScore to change the value to which it points. The following line is completely legal.

```c
*pScore = 500;
```

Confused? Don't be. It's perfectly fine to use a constant pointer to change the value to which it points. Remember, the restriction on a constant pointer is that its value—the address that the pointer stores—can't change.

The way a constant pointer works should remind you of something—a reference. Like a reference, a constant pointer can refer only to the object it was initialized to refer to.

> Hint
> 
> Although you can use a constant pointer instead of a reference in your programs, you should stick with references when possible. References have a cleaner syntax than pointers and can make your code easier to read.

## Using a Pointer to a Constant

As you've seen, you can use pointers to change the values to which they point. However, by using the const keyword when you declare a pointer, you can restrict a pointer so it can't be used to change the value to which it points. A pointer like this is called a pointer to a constant. Here's an example of declaring such a pointer:

```c
const int* pNumber; //a pointer to a constant
```

The preceding code declares a pointer to a constant, pNumber. You declare a pointer to a constant by putting const right before the type of value to which the pointer will point.

You assign an address to a pointer to a constant as you did before.

```c
int lives = 3;
pNumber = &lives;
```

However, you can't use the pointer to change the value to which it points. The following line is illegal.

```c
*pNumber = 1; //illegal -- can't use pointer to a constant to change value
//that pointer points to
```

Although you can't use a pointer to a constant to change the value to which it points, the pointer itself can change. This means that a pointer to a constant

can point to different objects in a program. The following code is perfectly legal.

```c
const int MAX_LIVES = 5;
pNumber = &MAX_LIVES; //pointer itself can change
```

## Using a Constant Pointer to a Constant

A constant pointer to a constant combines the restrictions of a constant pointer and a pointer to a constant. This means that a constant pointer to a constant can only point to the object that it was initialized to point to. In addition, it can't be used to change the value of the object to which it points. Here's the declaration and initialization of such a pointer:

```c
const int* const pBONUS = &BONUS; //a constant pointer to a constant
```

The preceding code creates a constant pointer to a constant named pBONUS that points to the constant BONUS.

> Hint
> 
> Like a pointer to a constant, a constant pointer to a constant can point to either a non-constant or constant value.

You can't reassign a constant pointer to a constant. The following line is not legal.

```c
pBONUS = &MAX_LIVES; //illegal -- pBONUS can't point to another object
```

You can't use a constant pointer to a constant to change the value to which it points. This means that the following line is illegal.

```c
*pBONUS = MAX_LIVES; //illegal -- can't change value through pointer
```

In many ways, a constant pointer to a constant acts like a constant reference, which can only refer to the value it was initialized to refer to and which can't be used to change that value.

> Hint
> 
> Although you can use a constant pointer to a constant instead of a constant reference in your programs, you should stick with constant references when possible. References have a cleaner syntax than pointers and can make your code easier to read.

that holds my pitifully low score and another that holds your impressively high score. After displaying the scores, the program calls a function meant to swap the scores. Because only copies of the score values are sent to the function, the original variables are unaltered. Next, the program calls another swap function. This time, through the use of constant pointers, the original variables' values are successfully exchanged (giving me the great big score and leaving you with the small one). Figure 7.3 shows the program in action.

![](img/c7e8651578bccd573227f684823b8754_257_0.png)

Figure 7.3
Passing pointers allows a function to alter variables outside of the function's scope.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 7 folder; the filename is swap_pointer_ver.cpp.

```c
// Swap Pointer
// Demonstrates passing constant pointers to alter argument variables

#include <iostream>

using namespace std;

void badSwap(int x, int y);
void goodSwap(int* const pX, int* const pY);

int main()
{
int myScore = 150;
int yourScore = 1000;
cout << "Original values\n";
cout << "myScore: " << myScore << "\n";
cout << "yourScore: " << yourScore << "\n\n";

cout << "Calling badSwap()\n";
badSwap(myScore, yourScore);
cout << "myScore: " << myScore << "\n";
cout << "yourScore: " << yourScore << "\n\n";

cout << "Calling goodSwap()\n";
goodSwap(&myScore, &yourScore);
cout << "myScore: " << myScore << "\n";
cout << "yourScore: " << yourScore << "\n";

return 0;
}

void badSwap(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
}

void goodSwap(int* const pX, int* const pY)
{
    //store value pointed to by pX in temp
    int temp = *pX;
    //store value pointed to by pY in address pointed to by pX
    *pX = *pY;
    //store value originally pointed to by pX in address pointed to by pY
    *pY = temp;
}
```

## Passing by Value

After I declare and initialize myScore and yourScore, I send them to cout. As you'd expect, 150 and 1000 are displayed. Next I call badSwap(), which passes both

By starting the header with string*, I'm saying that the function will return a pointer to a string object (and not a string object itself). To specify that a function returns a pointer to an object of a particular type, put an asterisk after the type name of the return type.

The body of the function ptrToElement() contains only one statement, which returns a pointer to the element at position i in the vector pointed to by pVec.

```c
return &((*pVec)[i]);
```

The return statement might look a little cryptic, so I'll step through it. Whenever you come upon a complex expression, evaluate it like the computer does—by starting with the innermost part. I'll start with (*pVec)[i], which means the element in position i of the vector pointed to by pVec. By applying the address of operator (&) to the expression, it becomes the address of the element in position i of the vector pointed to by pVec.

## Trap

Although returning a pointer can be an efficient way to send information back to a calling function, you have to be careful not to return a pointer that points to an out-of-scope object. For example, the following function returns a pointer that, if used, could crash the program.

```c
string* badPointer()
{
    string local = "This string will cease to exist once the function ends.";
    string* pLocal = &local;
    return pLocal;
}
```

That's because badPointer() returns a pointer to a string that no longer exists after the function ends. A pointer to a non-existent object is called a dangling pointer. Attempting to dereference a dangling pointer can lead to disastrous results. One way to avoid dangling pointers is to never return a pointer to a local variable.

## Using a Returned Pointer to Display a Value

After I create inventory, a vector of items, I display a value with a returned pointer.

```c
cout << *(ptrToElement(&inventory, 0)) << "\n\n";
```

The preceding code calls ptrToElement(), which returns a pointer to inventory[0]. (Remember, ptrToElement() doesn't return a copy of one of the elements of
