
is the same, as is the sequence of additional output numbers. Consequently, pseudorandom-number generators need some sort of seed that changes in an apparently random fashion. Fortunately, the second component of the current time is a changeable input that appears random when used correctly. When you run an application, most likely you won’t start running it at precisely the same second in time. The RandomNumber example shown in Listing 2-7 shows how to generate a random number.

### LISTING 2-7: Seeding the Random-Number Generator

```cpp
#include <iostream>
#include <time.h>
#include <stdlib.h>

using namespace std;

int main()
{
    // Seed the random-number generator
    time_t now;
    time(&now);
    srand(now);

    // Print out a list of random numbers
    for (int i=0; i<5; i++)
    {
        cout << rand() % 100 << endl;
    }

    return 0;
}
```

The example follows a process that you often see when working with random numbers. To obtain the time, you must include time.h. Initializing and using the random-number generator requires that you include stdlib.h.

- Obtain the current time to start the random-number generator by creating a variable called `now` of a special type called `time_t` (which is just a number).
- Call the `time()` function, passing the address of `now`, which obtains the number of seconds since January 1, 1970.
- Initialize the random number using the time seed by calling `srand()`.
- Create a random number based on the seed by calling `rand()`.

Each time you call `rand()`, you receive a new random int. However, the number may not be in the range you want. To limit the numbers in the range from 0 through 99, the code uses the *modulus 100* of the number. (That’s the remainder when you divide the number by 100.) The first time you run Listing 2-7, you may see the following output:

```
19
69
85
83
47
```

The second time, you may see this output. It’s different than before:

```
79
67
38
72
73
```

## Storing Data in Arrays

Most programming languages support a data structure called an array. An *array* is a list of variables, all stored side by side in a row. You access them through a single name. Each variable in the array must be of the same type. This section tells you how to work with arrays for data storage purposes in a simple manner. A more detailed discussion of creating and using arrays in an advanced way appears in the “Building Up Arrays” section of Book 5, Chapter 1.

When you create an array, you specify how many items the array holds. For example, you can have an array of 100 integers. Or you can have an array of 35 strings or an array of 10 pointers to the class `BrokenBottle`. If the code you’re working with represents a type, you can create an array out of it.

When you create an array, you give it a name. You can access the array’s *elements* (items) by using that name followed by an *index* number in brackets. The first element is always 0. Thus, if you have an array of five integers called `AppendixAttacks`, the first element is `AppendixAttacks[0]`. The second is `AppendixAttacks[1]`, and then `AppendixAttacks[2]`, `AppendixAttacks[3]`, and finally `AppendixAttacks[4]`.

![](img/128ab511de4e7360e167e3b15cdd5dd0_322_0.png)

Because an array starts with element number 0, the final element in the array has an index that is 1 less than the size of the array. Thus, an array of 89 elements has indexes ranging from 0 to 88.

### Declaring and accessing an array

Here’s how you declare an array:

```cpp
int GrilledShrimp[10];
```

This line declares an array of 10 integers called `GrilledShrimp`. You first put the type (which is really the type of each element in the array), and then the name for the array, and then the number of elements in brackets. And because this declares 10 integers, their indexes range from 0 to 9.

To access the first element of the array, you put the number 0 in brackets after the array name, as in

```cpp
GrilledShrimp[0] = 10;
```

Often, people use a loop to fill in an array or access each member. People usually call this *looping through the array*. The ArrayLoop example, in Listing 2-8, shows how to create and use a basic array.

### LISTING 2-8: Using a Loop to Loop Through the Array

```cpp
#include <iostream>

using namespace std;

int main() {
    int Values[5];
    int VSize = sizeof(Values)/sizeof(*Values);
    cout << "Array count: " << VSize << endl;

    for (int i=0; i < VSize; i++) {
        Values[i] = i * 2;
        cout << Values[i] << endl;
    }

    return 0;
}
```

**REMEMBER:** It’s never a good idea to hard-code the length of your array anywhere in your code because the array length could change. Rather, calculate the size of the array using the `sizeof()` function. The example shows you how to perform this task by obtaining the actual length of Values in bytes and dividing it by the size of the individual array elements, which requires `*Values`. The result, VSize, is the number of array elements. When you use a for loop to loop through the array, you set the counter variable, i, to end the loop when it equals or exceeds the value of VSize.

**WARNING:** When you use arrays, don’t go beyond the array bounds. Due to some old rules of the early C language, the compiler doesn’t warn you if you write a loop that goes beyond the upper boundary of an array. You may not get an error when you run your application, either.

### Arrays of pointers

Arrays are particularly useful for storing pointers — a variable that contains the address of an item in memory — to objects. If you have lots of objects of the same type, you can store them in an array.

Although you can store the actual objects in the array, most people don’t because they take up too much space. Most people fill the array with pointers to the objects. To declare an array of pointers to objects, remember the asterisk in the type declaration, like this:

```cpp
CrackedMusicCD *missing[10];
```

The ArrayPointer example, shown in Listing 2–9, declares an array of pointers. In this example, after declaring the array, you fill the elements of the array with zeroes. Remember that each element is a pointer; that way, you can immediately know whether the element points to something by just comparing it to 0. If it’s 0, it’s not being used. If it has something other than 0, it has a pointer in it.

### LISTING 2-9: Using an Array to Store a List of Pointers to Your Objects

```cpp
#include <iostream>

using namespace std;

class CrackedMusicCD {
public:
  string FormerName;
  int FormerLength;
  int FormerProductionYear;
};

int main() {
    CrackedMusicCD *Missing[10];
    int SMissing = sizeof(Missing)/sizeof(*Missing);

    for (int i=0; i < SMissing; i++) {
        Missing[i] = 0;
    }
    return 0;
}
```

If you want to create a whole group of objects and fill the array with pointers to these objects, you can do this kind of thing:

```cpp
for (int i=0; i < SMissing; i++) {
    Missing[i] = new CrackedMusicCD;
}
```

Because each element in the array is a pointer, if you want to access the properties or methods of one of the objects pointed to by the array, you need to *dereference* the pointer — obtain the value pointed to by the pointer — by using the **->** notation:

```cpp
Missing[0]->FormerName = "Shadow Dancing by Andy Gibb";
```

This sample line accesses the FormerName property of the object whose address is in the first position of the array. When you’re finished with the object pointers in the array, you can delete the objects by calling `delete` for each member of the array, as in this example:

```cpp
for (int i=0; i < SMissing; i++) {
    delete Missing[i];
    Missing[i] = 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_324_0.png)

The preceding code clears each array element to 0. That way, the pointer is reset to 0 and no longer points to anything after its object is gone.

### Passing arrays to functions

Sometimes you need to pass an entire array to a function. Though passing entire objects to functions can be unwieldy, passing an entire array can be dangerous. Arrays can be enormous, with thousands of elements. If each element is a pointer, each element could contain several bytes, which works with smaller arrays, but could cause problems with arrays containing thousands of elements. When you pass a huge array on the stack, you may *overflow* the application’s stack — meaning the application crashes. Fortunately, the compiler automatically treats arrays as pointers for you, but you still need to understand what is happening underneath the covers.

As with passing objects, your best bet is to pass an array’s address. You pass the function a pointer to the array. But passing an array’s address to a function is confusing to code. The ArrayPassing example, shown in Listing 2-10, is a sample that passes an array, without directly coding any pointers and addresses.

### LISTING 2-10: Passing an Array to a Function by Declaring the Array in the Function Header

```cpp
#include <iostream>

using namespace std;

const int MyArraySize = 10;

void Crunch(int myarray[], int size) {
    for (int i=0; i<size; i++) {
        cout << myarray[i] << endl;
    }
}

int main() {
    int BigArray[MyArraySize];

    for (int i=0; i<MyArraySize; i++)
    {
        BigArray[i] = i * 2;
    }

    Crunch(BigArray, MyArraySize);
    return 0;
}
```
