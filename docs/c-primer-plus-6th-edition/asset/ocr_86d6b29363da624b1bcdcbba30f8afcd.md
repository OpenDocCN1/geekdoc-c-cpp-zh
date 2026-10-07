# Listing 7.5 arrfun1.cpp

```
// arrfun1.cpp -- functions with an array argument
#include <iostream>
const int ArSize = 8;
int sum_arr(int arr[], int n); // prototype
int main() {
    nusing namespace std;
    int cookies(ArSize) = {1,2,4,8,16,32,64,128};
    // some systems requiring preceding int with static to
    // enable array initialization

    int sum = sum_arr(cookies, ArSize);
    cout << "Total cookies eaten: " << sum << "\n";
    return 0;
}

// return the sum of the integer array
int sum_arr(int arr[], int n)
{
    int total = 0;
    for (int i = 0; i < n; i++)
        total = total + arr[i];
    return total;
}
```

Here is the output of the program in Listing 7.5:
Total cookies eaten: 255

As you can see, the program works. Now let's look at why it works.

# How Pointers Enable Array-Processing Functions

The key to program in Listing 7.5 is C++, like C, in most contexts treat the name of an array as if it were a pointer. Recall from Chapter 4, "Compound Types," that C++ interprets an array name as the address of its first element:
cookies = &cookies[0] // array name is address of first

(There are a few exceptions to this rule. First, the array declaration uses the array name to label the storage. Second, applying sizeof to an array name yields the size of the array in bytes. Third, as mentioned in Chapter 4, applying the address operator & to an array name returns the address of the whole array, for example, &cookies would be the address of a 32-byte block of memory if int is 4 bytes.)