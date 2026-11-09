
- 1. Change the program to loop over our text 100 times

### Example Using Counter Inside Loop

We can use our declared integer inside the associated block of code, for example, we could print the value 1 to 10 with the code below.

```cpp
#include<iostream>
using namespace std;

int main(){

    for(int i = 1 ; i <= 10; i++){
        cout << i << endl;
    }

    return 0;
}
```

![](img/443990a0ec620659ce8be783c0758bc6_74_0.png)

## while loops

**while** loops are similar to *for* loops, with the only difference being that it is only the condition to be met that is in the parenthesis associated with the while keyword.

### Example

![](img/443990a0ec620659ce8be783c0758bc6_75_0.png)

### Explanation

We first declare where we will start counting from in the line: **int i = 1;**

**while(i <= 10)**, means while the value of the variable *i* is less or equal to 10 run the associated block of code.

Notice that just before the closing brace we increment the value of i by 1.

The while loop then repeats to check whether i is less or equal to 10, if it is, it executes the associated block of code. If i is greater than 10, the block of code is not executed, and the program goes to the next instructions.

## Infinite loops

Infinite loops occur when the condition that *for* loop or *while* loop checks in order to decide whether to run their associated block of code, is always **true**. **So, it basically runs forever.**

### Example

```cpp
#include<iostream>
using namespace std;

int main(){

    while( true ){
        cout << "Hi from the infinite while loop" << endl;
    }

    return 0;
}
```

```
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
Hi from the infinite while loop
```

### Explanation

This will run forever as the condition is always true.

### Infinite For Loop

An infinite for loop is defined as shown below:

```cpp
#include<iostream>
using namespace std;

int main()
{
    for(;;){
        cout << "Hi from the infinite for loop" << endl;
    }

    return 0;
}
```

![](img/443990a0ec620659ce8be783c0758bc6_79_0.png)

### Explanation

Notice that to declare an infinite for loop, you just need to have two semicolons in the parentheses associated with the for keyword, that is:

```cpp
for(;;){
    //this code will run infinitely
}
```

### Exercise

- 1. Rewrite the following loops as for loops.

  - a.

    ```cpp
    int x = 2;
    while(x <= 200)
    {
        if (x < 10 && x != 1)
            cout << "YY";
        x = x + 2;
    }
    ```

  - b.

    ```cpp
    int a = 2;
    while(a <= 21)
    {
        cout << "YY";
        a++;
    }
    ```

- 2. What is the output of the following (when embedded in a complete program)?

  ```cpp
  for (int ctr = 2; ctr < 15; ctr++)
      cout << (3 + ctr) << endl;
  ```

- 3. What is the output of the following?

  ```cpp
  for (int b = 50; b > 2; b = b - 3)
  {
      cout << "Hi ";
      cout << b << endl;
  }
  ```

- 4. Write a program that create prints out your name an infinite number of times using a for loop.

## Arrays

An array is a collection of values of the same data type.

Each value in the collection has an index associated with it that can be used to retrieve the value.

Indices in C++ start from 0 not 1, this is known as ***zero based indexing.*** It is like starting to count from 0 and not 1.

### Exercise

How many items do I have, if I gave them labels from 0 to 4?

**Answer: 5**

### Declaring an array

When declaring an array, we begin by specifying the data type of the values that the array will hold followed by the variable name of the array then by the number of elements it will hold in square brackets.

For example:

```cpp
int size[4];
size = {1, 2, 3, 4};
```

### Explanation

Above we have declared an array with the variable name *size* which holds 4 values of the data type integer.

```cpp
int size[4];
```

### Retrieving values from an array

Values are retrieved from an array by specifying the location of the needed value using an index.

### Example

Let's say we want to retrieve the first element in an array, our code would be:

```cpp
#include<iostream>
using namespace std;

int main(){
    int size[4] = {1, 2, 3, 4};
    int firstElement = size[0];

    cout << firstElement ;
    return 0;
}
```

![](img/443990a0ec620659ce8be783c0758bc6_84_0.png)

### Explanation

The line, `int firstElement = size[0];`, retrieves the first element in the array.

Notice that since in C++ we start counting from 0, the index of the first element in the array is 0. The program prints out 1 since the 1ˢᵗ element in size is 1.

### Exercise

Retrieve the fourth element. (Hint the index is not 4)

### Looping through elements in an array

If we want to retrieve all the elements in an array, we can use loops to do that.
We will use *for* loop since it is the simplest way to go about it.

### Example

```cpp
#include<iostream>
using namespace std;

int main(){
    int size[4] = {1, 2, 3, 4};

    for(int i = 0 ; i < 4; i++){
        cout << size[i] ;
    }
    return 0;
}
```

![](img/443990a0ec620659ce8be783c0758bc6_86_0.png)

### Explanation

Notice that we start our counter from 0 and our condition is that the value of the counter *i* should be less than 4, which is the size of the array.

### Exercise

This is to be done in one file:

- 1. Write a function that calculates the area of a circle.
- 2. Create an array that holds 10 circle radii that you want to know the areas of.
- 3. Loop through the array to calculate the areas of the circles and print the result to the screen.
- 4. Calculate only the area of the circle in the fourth position in the array.
- 5. Create an array of the character of your name and print all of the characters to the screen.

## Structures

A structure is a group of values that enables you to order data in a logical manner, that is, in a manner that makes sense to you.

Let's say that you want to collect information about your friends’ age, weight and height.

With the current knowledge we have we would do it something like this:

### Example code

```cpp
#include<iostream>
using namespace std;

int main(){
    int kevinAge = 10;
    int kevinWeight = 30;
    int kevinHeight = 1;

    int jessicaAge = 15;
    int jessicaWeight = 20;
    int jessicaHeight = 1;
}
```

Structures make grouping such information easier.

Let's first define a structure.

### Structure definition

![](img/443990a0ec620659ce8be783c0758bc6_89_0.png)

### Explanation

A structure is defined outside any function definition, including the main function.

We use the keyword **struct** to define a structure followed by the name we want to give the structure, this name is known as a *structure tag*.

Inside the curly braces associated with the structure tag, we declare structure variables which are also known as *member names*. In the above example, **age**, **weight** and **height** are *member names*.

Notice that there is a semicolon after the closing curly brace.

### Initializing structures

```cpp
#include<iostream>
using namespace std;

struct PersonInfo{
    int age;
    int weight;
    int height;
};

int main(){
    // initializing the structure
    PersonInfo kevin = {10, 30, 1};
    PersonInfo jessica = {15, 28, 1};

    return 0;
}
```
