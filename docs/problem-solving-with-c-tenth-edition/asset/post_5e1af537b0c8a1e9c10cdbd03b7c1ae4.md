
# DISPLAY 7.3 Indexed Variable as an Argument (part 2 of 2)

## Sample Dialogue

```
Enter allowed vacation days for employees 1 through 3:
10 20 5
The revised number of vacation days are:
Employee number 1 vacation days = 15
Employee number 2 vacation days = 25
Employee number 3 vacation days = 10
```

## SELF-TEST EXERCISES

11. Consider the following function definition:

```
void tripler(int& n)
{
    n = 3*n;
}
```

Which of the following are acceptable function calls?

```
int a[3] = {4, 5, 6}, number = 2;
tripler(number);
tripler(a[2]);
tripler(a[3]);
tripler(a[number]);
tripler(a);
```

12. What (if anything) is wrong with the following code? The definition of tripler is given in Self-Test Exercise 11.

```
int b[5] = {1, 2, 3, 4, 5};
for (int i = 1; i <= 5; i++)
    tripler(b[i]);
```

# Entire Arrays as Function Arguments

A function can have a formal parameter for an entire array so that when the function is called, the argument that is plugged in for this formal parameter is an entire array. However, a formal parameter for an entire array is neither a call-by-value parameter nor a call-by-reference parameter; it is a new kind of formal parameter referred to as an array parameter. Let’s start with an example.

![](img/88b1f375f11336dbd9dac8b1675d0698_427_0.png)

The function defined in Display 7.4 has one array parameter, a, which will be replaced by an entire array when the function is called. It also has one ordinary call-by-value parameter (size) that is assumed to be an integer value equal to the size of the array. This function fills its array argument (that is, fills all the array’s indexed variables) with values typed in from the keyboard, and then the function outputs a message to the screen telling the index of the last array index used.

The formal parameter `int a[ ]` is an array parameter. The square brackets, with no index expression inside, are what C++ uses to indicate an array parameter. An array parameter is not quite a call-by-reference parameter, but for most practical purposes it behaves very much like a call-by-reference parameter. Let’s go through this example in detail to see how an array argument works in this case. (An array argument is, of course, an array that is plugged in for an array parameter, such as `a[ ]`.)

When the function `fillUp` is called it must have two arguments. The first gives an array of integers, and the second should give the declared size of the array. For example, the following is an acceptable function call:

```cpp
int score[5], numberOfScores = 5;
fillUp(score, numberOfScores);
```

This call to `fillUp` will fill the array `score` with five integers typed in at the keyboard. Notice that the formal parameter `a[ ]` (which is used in the function declaration and the heading of the function definition) is given with square brackets, but no index expression. (You may insert a number inside the square brackets for an array parameter, but the compiler will simply ignore

# DISPLAY 7.4 Function with an Array Parameter

**Function Declaration**

```cpp
1   void fillUp(int a[], int size);
2   //Precondition: size is the declared size of the array a.
3   //The user will type in size integers.
4   //Postcondition: The array a is filled with size integers
5   //from the keyboard.
```

**Function Definition**

```cpp
1   //Uses iostream:
2   void fillUp(int a[], int size)
3   {
4       using namespace std;
5       cout << "Enter " << size << " numbers:\n";
6       for (int i = 0; i < size; i++)
7           cin >> a[i];
8       size--;
9       cout << "The last array index used is " << size << endl;
10  }
```

the number, so we do not use such numbers in this book.) On the other hand, the argument given in the function call (score in this example) is given without any square brackets or any index expression. What happens to the array argument score in this function call? Very loosely speaking, the argument score is plugged in for the formal array parameter a in the body of the function, and then the function body is executed. Thus, the function call

```
fillUp(score, numberOfScores);
```

is equivalent to the following code:

```
{
    using namespace std;
    size = 5;
    cout << "Enter " << size << " numbers:\n";
    for (int i = 0; i < size; i++)
        cin >> score[i];
    size--;
    cout << "The last array index used is " << size << endl;
}
```

5 is the value of numberOfScores

The formal parameter a is a different kind of parameter from the ones we have seen before now. The formal parameter a is merely a placeholder for the argument score. When the function fillUp is called with score as the array argument, the computer behaves as if a were replaced with the corresponding argument score. When an array is used as an argument in a function call, any action that is performed on the array parameter is performed on the array argument, so the values of the indexed variables of the array argument can be changed by the function. If the formal parameter in the function body is changed (for example, with a cin statement), then the array argument will be changed.

So far it looks like an array parameter is simply a call-by-reference parameter for an array. That is close to being true, but an array parameter is slightly different from a call-by-reference parameter. To help explain the difference, let’s review some details about arrays.

Recall that an array is stored as a contiguous chunk of memory. For example, consider the following declaration for the array score:

```
int score[5];
```

When you declare this array, the computer reserves enough memory to hold five variables of type int, which are stored one after the other in the computer’s memory. The computer does not remember the addresses of each of these five indexed variables; it remembers only the address of indexed variable score[0]. For example, when your program needs score[3], the computer calculates the address of score[3] from the address of score[0]. The computer knows that score[3] is located three int variables past score[0]. Thus, to obtain the address of score[3], the computer takes the address of score[0] and adds a number that represents the amount of memory used by three int variables; the result is the address of score[3].

Arrays in memory

# Array argument

Viewed this way, an array has three parts: the address (location in memory) of the first indexed variable, the base type of the array (which determines how much memory each indexed variable uses), and the size of the array (that is, the number of indexed variables). When an array is used as an array argument to a function, only the first of these three parts is given to the function. When an array argument is plugged in for its corresponding formal parameter, all that is plugged in is the address of the array's first indexed variable. The base type of the array argument must match the base type of the formal parameter, so the function also knows the base type of the array. However, the array argument does not tell the function the size of the array. When the code in the function body is executed, the computer knows where the array starts in memory and how much memory each indexed variable uses, but (unless you make special provisions) it does not know how many indexed variables the array has. That is why it is critical that you always have another int argument telling the function the size of the array. That is also why an array parameter is not the same as a call-by-reference parameter. You can think of an array parameter as a weak form of call-by-reference parameter in which everything about the array is told to the function except for the size of the array.²

# Different size array arguments can be plugged in for the same array parameter

These array parameters may seem a little strange, but they have at least one very nice property as a direct result of their seemingly strange definition. This advantage is best illustrated by again looking at our example of the function fillUp given in Display 7.4. That same function can be used to fill an array of any size, as long as the base type of the array is int. For example, suppose you have the following array declarations:

```
int score[5], time[10];
```

The first of the following calls to fillUp fills the array score with five values and the second fills the array time with ten values:

```
fillUp(score, 5);
fillUp(time, 10);
```

You can use the same function for array arguments of different sizes because the size is a separate argument.

# The const Parameter Modifier

When you use an array argument in a function call, the function can change the values stored in the array. This is usually fine. However, in a complicated function definition, you might write code that inadvertently changes one or more of the values stored in an array, even though the array should not be changed at all. As a precaution, you can tell the compiler that you do not

> ²If you have heard of pointers, this will sound like pointers, and indeed an array argument is passed by passing a pointer to its first (zeroth) index variable. We will discuss this in Chapter 9. If you have not yet learned about pointers, you can safely ignore this footnote.
