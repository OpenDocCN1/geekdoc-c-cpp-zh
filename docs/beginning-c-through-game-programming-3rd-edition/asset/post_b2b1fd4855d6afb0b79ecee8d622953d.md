
By starting the header with string*, I’m saying that the function will return a pointer to a string object (and not a string object itself). To specify that a function returns a pointer to an object of a particular type, put an asterisk after the type name of the return type.

The body of the function ptrToElement() contains only one statement, which returns a pointer to the element at position i in the vector pointed to by pVec.

```
return &((*pVec)[i]);
```

The return statement might look a little cryptic, so I’ll step through it. Whenever you come upon a complex expression, evaluate it like the computer does—by starting with the innermost part. I’ll start with (*pVec)[i], which means the element in position i of the vector pointed to by pVec. By applying the address of operator (&) to the expression, it becomes the address of the element in position i of the vector pointed to by pVec.

## Trap

Although returning a pointer can be an efficient way to send information back to a calling function, you have to be careful not to return a pointer that points to an out-of-scope object. For example, the following function returns a pointer that, if used, could crash the program.

```
string* badPointer()
{
    string local = "This string will cease to exist once the function ends.";
    string* pLocal = &local;
    return pLocal;
}
```

That’s because badPointer() returns a pointer to a string that no longer exists after the function ends. A pointer to a non-existent object is called a dangling pointer. Attempting to dereference a dangling pointer can lead to disastrous results. One way to avoid dangling pointers is to never return a pointer to a local variable.

## Using a Returned Pointer to Display a Value

After I create inventory, a vector of items, I display a value with a returned pointer.

```
cout << *(ptrToElement(&inventory, 0)) << "\n\n";
```

The preceding code calls ptrToElement(), which returns a pointer to inventory[0]. (Remember, ptrToElement() doesn’t return a copy of one of the elements of inventory; it returns a pointer to one of them.) The line then sends the string object pointed to by the pointer to cout. As a result, sword is displayed.

## Assigning a Returned Pointer to a Pointer

Next I assign a returned pointer to another pointer with the following line.

```
string* pStr = ptrToElement(&inventory, 1);
```

The call to ptrToElement() returns a pointer to inventory[1]. The statement assigns that pointer to pStr. This is an efficient assignment because assigning a pointer to a pointer does not involve copying the string object.

To help you understand the results of this line of code, look at Figure 7.5, which shows a representation of pStr after the assignment. (Note that the figure is abstract because the vector inventory doesn’t contain the string literals "sword", "armor", and "shield"; instead, it contains string objects.)

![](img/34f09be0ed6217c465debc4490197d4f_264_0.png)

Figure 7.5
pStr points to the element at position 1 of inventory.

Next I send *pStr to cout and armor is displayed.

## Assigning to a Variable the Value Pointed to by a Returned Pointer

Next I assign the value pointed to by a returned pointer to a variable.

```
string str = *(ptrToElement(&inventory, 2));
```

The call to ptrToElement() returns a pointer to inventory[2]. However, the preceding statement doesn’t assign this pointer to str—it can’t because str is a string object. Instead, the computer quietly makes a copy of the string object to which the pointer points and assigns that object to str. To help drive this point home, check out Figure 7.6, which provides an abstract representation of the results of this assignment.

![](img/34f09be0ed6217c465debc4490197d4f_265_0.png)

# Figure 7.6

str is a new string object, totally independent from inventory.

An assignment like this one, where an object is copied, is more expensive than the assignment of one pointer to another. Sometimes the cost of copying an object is perfectly acceptable, but you should be aware of the extra overhead associated with this kind of assignment and avoid it when necessary.

## Altering an Object through a Returned Pointer

You can also alter the object to which a returned pointer points. This means that I can change the hero’s inventory through pStr.

```
*pStr = "Healing Potion";
```

Because pStr points to the element in position 1 of inventory, this code changes inventory[1] so it’s equal to "Healing Potion". To prove this, I display the element with the following line, which does indeed show Healing Potion.

```
cout << inventory[1] << endl;
```

For an abstract representation, check out Figure 7.7, which shows the status of the variables after the assignment.

## Hint

If you want to protect an object pointed to by a returned pointer, make sure to restrict the pointer. Return either a pointer to a constant or a constant pointer to a constant.

## inventory

![](img/34f09be0ed6217c465debc4490197d4f_266_0.png)

Figure 7.7
inventory[1] is changed through the returned pointer stored in pStr.

## UNDERSTANDING THE RELATIONSHIP BETWEEN POINTERS AND ARRAYS

Pointers have an intimate relationship with arrays. In fact, an array name is really a constant pointer to the first element of the array. Because the elements of an array are stored in a contiguous block of memory, you can use the array name as a pointer for random access to elements. This relationship also has important implications for how you can pass and return arrays, as you’ll soon see.

## Introducing the Array Passer Program

The Array Passer program creates an array of high scores and then displays them, using the array name as a constant pointer. Next, the program passes the array name as a constant pointer to a function that increases the scores. Finally, the program passes the array name to a function as a constant pointer to a constant to display the new high scores. Figure 7.8 shows the results of the program.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 7 folder; the filename is array_passer.cpp.

```
//Array Passer
//Demonstrates relationship between pointers and arrays

#include <iostream>

using namespace std;
```

![](img/34f09be0ed6217c465debc4490197d4f_267_0.png)

# Figure 7.8

Using an array name as a pointer, the high scores are displayed, altered, and passed to functions.

```
void increase(int* const array, const int NUM_ELEMENTS);
void display(const int* const array, const int NUM_ELEMENTS);

int main()
{
    cout << "Creating an array of high scores.\n\n";
    const int NUM_SCORES = 3;
    int highScores[NUM_SCORES] = {5000, 3500, 2700};

    cout << "Displaying scores using array name as a constant pointer.\n";
    cout << *highScores << endl;
    cout << *(highScores + 1) << endl;
    cout << *(highScores + 2) << "\n\n";

    cout << "Increasing scores by passing array as a constant pointer.\n\n";
    increase(highScores, NUM_SCORES);

    cout << "Displaying scores by passing array as a constant pointer to a constant.\n";
    display(highScores, NUM_SCORES);

    return 0;
}
```

```
void increase(int* const array, const int NUM_ELEMENTS)
{
    for (int i = 0; i < NUM_ELEMENTS; ++i)
    {
        array[i] += 500;
    }
}
```

```
void display(const int* const array, const int NUM_ELEMENTS)
{
    for (int i = 0; i < NUM_ELEMENTS; ++i)
    {
        cout << array[i] << endl;
    }
}
```

## Using an Array Name as a Constant Pointer

Because an array name is a constant pointer to the first element of the array, you can dereference the name to get at the first element. That’s what I do after I create an array of high scores, called highScores.

```
cout << *highScores << endl;
```

I dereference highScores to access the first element in the array and send it to cout. As a result, 5000 is displayed.

You can randomly access array elements using an array name as a pointer through simple addition. All you have to do is add the position number of the element you want to access to the pointer before you dereference it. This is simpler than it sounds. For example, I next access the score at position 1 in highScores with the following line, which displays 3500.

```
cout << *(highScores + 1) << endl;
```

In the preceding code, *(highScores + 1) is equivalent to highScores[1]. Both return the element in position 1 of highScores.

Next, I access the score at position 2 in highScores with the following line, which displays 2700.

```
cout << *(highScores + 2) << endl;
```
