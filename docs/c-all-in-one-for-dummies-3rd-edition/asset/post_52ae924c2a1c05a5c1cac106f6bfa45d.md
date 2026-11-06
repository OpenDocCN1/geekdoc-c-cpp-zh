
## Book VI Chapter 1: Exploring the Standard Library Further

### Locating Values Using the Find Algorithm

The Standard Library contains a number of functions to find something you need within a container. Locating what you need as efficiently as possible is always a good idea. Unlike your closet, you want your applications well organized and easy to manage! The four common `find()` algorithms are

- `find()`
- `find_end()`
- `find_first_of()`
- `find_if()`

The algorithm you use depends on what you want to find and where you expect to find it. You’ll likely use the plain `find()` algorithm most often. The *FindString* example shows how to locate a particular string within a `vector` — you can use the same approach to locate something in any container type:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main()
{
    vector<string> Words;

    Words.push_back("Blue");
    Words.push_back("Green");
    Words.push_back("Teal");
    Words.push_back("Brick");
    Words.push_back("Purple");
    Words.push_back("Brown");
    Words.push_back("LightGray");

    vector<string>::iterator Result =
        find(Words.begin(), Words.end(), "LightGray");

    if (Result != Words.end())
        cout << *Result << endl;
    else
        cout << "Value not found!" << endl;

    Result = find(Words.begin(), Words.end(), "Black");

    if (Result != Words.end())
        cout << *Result << endl;
    else
        cout << "Value not found!" << endl;
}
```

The example starts with a `vector` containing color strings. In both cases, the code attempts to locate a particular color within the `vector`. The first time the

![](img/6ba99460b0feb3585671a4612ff5fabb_716_0.png)

Actually, not one of the random number generators in the Standard Library works properly — imagine that! They are all *pseudorandom* number generators: The numbers are distributed such that it appears that you see a random sequence, but given enough time and patience, eventually the sequence repeats. In fact, if you don’t set a seed value for your random number generator, you can obtain predictable sequences of numbers every time. How boring. Here is typical output from this example:

```text
The random month number is: ?
```

![](img/6ba99460b0feb3585671a4612ff5fabb_716_1.png)

The first line of code in `main()` sets the seed by using the system time. Using the system time ensures a certain level of randomness in the starting value — and therefore a level of randomness for your application as a whole. If you comment out this line of code, you see the same output every time you run the application. In our case, our system output 6 every time.

The example application uses `rand()` to create the random value. When you take the modulus of the random number, you obtain an output that is within a specific range — 12 in this case. The example ends by adding 1 to the random number because there isn’t any month 0 in the calendar, and then outputs the month number for you.

The Standard Library provides access to two types of pseudorandom number generators. The first type requires that you set a seed value. The second type requires that you provide an input value with each call and doesn’t require a seed value. Each generator outputs a different data type, so you can choose the kind of random number you obtain. Table 1-1 lists the random number generators and tells you what data type they output.

### Table 1-1 Pseudorandom Number Generator Functions

| Function | Output Type | Seed Required? |
|---|---|---|
| rand | integer | yes |
| drand48 | double | yes |
| erand48 | double | no |
| lrand48 | long | yes |
| nrand48 | long | no |
| mrand48 | signed long | yes |
| jrand48 | signed long | no |

Now that you know about the pseudorandom number generators, look at the seed functions used to prime them. Table 1-2 lists the seed functions and their associated pseudorandom number generator functions.

### Working with Temporary Buffers

Temporary buffers are useful for all kinds of tasks. Normally, you use them when you want to preserve the original data, yet you need to manipulate the data in some way. For example, creating a sorted version of your data is a perfect use of a temporary buffer. The TemporaryBuffer example shows how to use a temporary buffer to sort some strings.

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <algorithm>

using namespace std;

int main()
{
    vector<string> Words;

    Words.push_back("Blue");
    Words.push_back("Green");
    Words.push_back("Teal");
    Words.push_back("Brick");
    Words.push_back("Purple");
    Words.push_back("Brown");
    Words.push_back("LightGray");

    int Count = Words.size();
    cout << "Words contains: " << Count << " elements." << endl;

    // Create the buffer and copy the data to it.
    pair<string*, ptrdiff_t> Mem = get_temporary_buffer<string>(Count);

    uninitialized_copy(Words.begin(), Words.end(), Mem.first);

    // Perform a sort and display the results.
    sort(Mem.first, Mem.first+Mem.second);

    for (int i = 0; i < Mem.second; i++)
        cout << Mem.first[i] << endl;

    return 0;
}
```

The example starts with the now familiar list of color names. It then counts the number of entries in the vector and displays the count onscreen.

At this point, the code creates the temporary buffer using `get_temporary_buffer`. The output is a `pair`, with the first value containing a pointer to the string values and the second value containing the count of data elements. `Mem` doesn't contain anything — you have simply allocated memory for it.

The next task is to copy the data from the vector (`Words`) to the pair (`Mem`) using `uninitialized_copy`. Now that `Mem` contains a copy of your data, you can organize it using the `sort` function. The final step is to display the `Mem` content onscreen. Here is what you’ll see:

```text
Words contains: 7 elements.
Blue
Brick
Brown
Green
LightGray
Purple
Teal
```

## Chapter 2: Working with User-Defined Literals (UDLs)

### In This Chapter

- Considering the needs and uses for UDLs
- Using the UDL features of the Standard Library
- Developing custom UDLs

Previous chapters have discussed literals as a kind of constant. For example, in the expression X = 5, the number 5 is a literal constant. The constant X stands in for the value 5 in application code. Using a literal makes it possible to create code that states the use of a value clearly, rather than having code that is filled with mystery values that no one can figure out. In addition, using literals makes it possible to change constant values in one place, rather than in each place they’re needed in an application.

Up to this point, you have used every other kind of literal constant in the various examples except for User-Defined Literals (UDLs). Unlike other kinds of literal constants, a UDL isn’t defined as part of the C++ compiler — you create UDLs as needed to make your code more readable and easier to manage. In some cases, UDLs come with the libraries you use in C++, such as the Standard Library. This chapter does discuss UDLs that come as part of the Standard Library, but it also looks at how you’d create your own UDLs as needed.

![](img/6ba99460b0feb3585671a4612ff5fabb_720_0.png)

UDLs aren’t part of older C++ specifications. In fact, they first made an appearance in C++11. What this means is that you must configure Code::Blocks to use the features provided by C++11 by using the technique found in the “Configuring the IDE” section of Book IV, Chapter 6. If you don’t perform the configuration for each example in this chapter, you see error messages telling you that the default setup doesn’t provide the desired support.

### Understanding the Need for UDLs

The whole point of literals is to make code more readable and easier to maintain. However, built-in literals are limited to a few data types, summarized as follows:

- Integer
- Floating-point
