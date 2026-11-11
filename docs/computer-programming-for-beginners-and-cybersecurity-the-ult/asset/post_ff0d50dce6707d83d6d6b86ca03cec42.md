
`int *p = numbers;`

```cpp
cout << "Address of the first element is " << p << endl;
```

The output of that line of code is:

Address of the first element is 0059F710

To access the value stored in the address of the first element of the array using the pointer, run the following line of code:

```cpp
cout << "The value in the address is " << *p << endl;
```

The output of the code is:

The value in the address is 1.

To move to the next element of the array, you have to increase p value.

```cpp
p++;
```

Now it will point to the second element of the array:

```cpp
cout << "Address of the second element is " << p << endl;
```

```cpp
cout << "The value in the address is " << *p << endl;
```

The output is:

The address of the second element of the numbers array on my PC is 0059F714

The value in the address of the second element is 5.

For example, if user enters string ‘Concatenation’ then the application will output

‘ConcatenationnoitanetacnoC’

The following header files must be included in the main.cpp file:

```cpp
#include "stdafx.h"
#include <stdio.h>
#include <cctype>
#include <iostream>
#include <cstring>
```

The `<cstring>` header is needed for the string functions: `strcpy_s()`, `strcat_s()` and `strlen()`. The `<cctype>` header file is needed for the `toupper()` function.

I want to explain how I copied characters from the original string to a temporary string in reversed order.

First, I got the length of the original string, using the `strlen()` function.

```cpp
length = strlen(aWord);
```

Then in the loop, I copied the last character of the original string to the first place of the temporary string and so on.

Let us examine the code in the loop.

```cpp
for (i = 0; i < length; i++)
    temp[i] = aWord[length - (i + 1)];
```

If a user enters the word ‘Concatenation’ then the word length will be 13. The index of the first character in a string is 0, then the index of the last character of the string will be 12. It means that the index of the last character is length - 1.

A line of code that I placed in the loop is

```cpp
temp[i] = aWord[length - (i + 1)];
```

When i = 0, temp[i] will refer to the first character of the temp string.

At the same time (when i = 0) the `aWord[length - (i + 1)]` will refer to the `aWord[13 - (0 + 1)]` character and it will be `aWord[12]` that is the last character of the ‘Concatenation’ string.

When i = 1, the temp[1] will refer to the second character of the temp string and `aWord[13 - (1 + 1)]` will refer to the second from the end character of the ‘Concatenation’ string.

That way, we can copy all characters in reversed order.

When we have copied all the characters from the original string to the temp string, we need to add null to the end of the temp string, because a string in C++ must be terminated with null.

The line of code `temp[length] = '\0';` will do the job.

The whole code is included in [visual_studio_2017.zip](visual_studio_2017.zip).

```cpp
#include "stdafx.h"
#include <stdio.h>
#include <cctype>
#include <cstring>
#include <iostream>

int main()
{
    char more = 'Y';

    char prompt1[] = "\nEnter a word not more than 20 characters and press enter.\n";

    char prompt3[] = "\nDo you want to continue? Y/N\n";

    char aWord[20];

    char aCopy[40];

    int length = 0;
    char temp[20];
    int i;

    while (toupper(more) == 'Y')
    {
        std::cout << prompt1;
        std::cin >> aWord;
        std::cout << "aWord=" << aWord << std::endl;
        strcpy_s(aCopy, aWord);
        std::cout << "aCopy=" << aCopy << std::endl;
        length = strlen(aWord);
        std::cout << "length=" << length << std::endl;

        // fill temp[] array with the word characters in opposite order.
        for (i = 0; i < length; i++)
            temp[i] = aWord[length - (i + 1)];
        temp[length] = '\0';
        std::cout << "Temp=" << temp << std::endl;
        strcat_s(aCopy, temp);
        std::cout << "aCopy after concatenation of temp=" << aCopy << std::endl;

        std::cout << prompt3;
        std::cin >> more;
    }

    return 0;
}
```

Output:

![](img/ecb1bfa35f80f656f92811abb43b3df7_223_0.png)

Figure String manipulation.

## Lists

Let us imagine a puzzle. You have a row of boxes. Each box contains a card with one letter. You have to figure out the sequence of the letters, so that the letters compose a word.

![](img/ecb1bfa35f80f656f92811abb43b3df7_223_1.png)

Figure A linked list

In the table above, you can see that each box has a number. You may guess that these numbers are the key to the puzzle. The first box has a letter T inside and number 5 on the front side. Take a card with the letter T and put it aside. The number 5 may point to the next letter. Count boxes. The fifth box has the letter ‘E.’ Take the card with the ‘E’ letter and place it next to T. You will get "TE." The box with the letter ‘E’ has number 2 on its side. So, take the card from the 2nd box and place it next to "TE." You will get "TEC."

The box with the letter ‘C’ has the number 10, so take the card from the 10th box. You will get "TECH." The box with the letter ‘H’ has number 4, so take the card from the 4th box. You got "TECHN." Continue following the numbers, and you will get the whole word: TECHNOLOGY.

That is how a linked list works. It is made of nodes. Each node has at least one variable that holds data (a text or number or object) and one variable (pointer) that holds the address of the next node. This system walks through the node list as you did in the puzzle. The pointer of the last node has null value, or it may point to the first node. Then we have a closed linked list.

### ADD A NODE

If you want to add a new node to the end of the linked list, you have to create a new node. Then point the pointer of the last node to the address of the new node and assign null to the new node pointer.

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_0.png)

Figure Adding a node to the end of the linked list.

If you want to add a new node to the beginning of the linked list, you have to create a new node. Point the pointer of the new node to the first node, and that is it.

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_1.png)

Figure Adding a node to the head of the linked list.

If you need to add a node in the middle of the linked list, you have to create a new node, and then break the chain: redirect the node (previous to the break) to a new node and point the pointer of the new node to the next node (the one after the break).

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_2.png)

Figure Adding a node in the middle of the linked list.

### DELETE A NODE

To delete a node with a certain key, you walk along with the list until you find the key. Then you assign the key node to the temp node. Then you point the node previous to the key node to the node next to the key node. See Figure 60. As a result, the temp key becomes isolated from the list. Now you can delete the temp.

![](img/ecb1bfa35f80f656f92811abb43b3df7_225_0.png)

Figure Delete a node.

Below is a code for Node class. For simplicity sake, I created a node that holds an integer and node pointer to the next node. Both class member variables are declared as private. It is good programming practice not to use global variables, because private members cannot be seen from the outside of the class. We still need to set and to read these private member variables. The public functions set and get will do the job.

## CHAPTER 3: Binary trees

Binary trees are one of the most useful of all the basic data structures and are by far the most interesting. They are the perfect example of how recursion and pointers can be used to do some very useful things.

One of the best techniques for creating lists of things is the linked list, but finding an element in the list can take a while. And, if you have a large amount of unstructured data, an array won’t help much either. You can try sorting the array but, even so, inserting items into it will still be difficult. If you have an array that you want to keep sorted, inserting new elements will take a lot of shuffling! And trying to find things in a list as quickly as possible is quite important, especially in scenarios like these:

- You’re building an MMORPG game and players need to be able to sign in quickly—that involves quickly looking players up
- You’re building software to process credit cards and millions of transactions need to be handled hourly—credit card balances need to be found very quickly
- You’re using a low-power device, such as a tablet or smartphone, and showing your users an address book. You don’t want your users to keep hanging because your data structure is slow.

This section will discuss the tools needed to overcome these problems and more.

The idea of the solution is to be able to store elements in a structure like a linked list, using pointers to help structure the memory, but in
