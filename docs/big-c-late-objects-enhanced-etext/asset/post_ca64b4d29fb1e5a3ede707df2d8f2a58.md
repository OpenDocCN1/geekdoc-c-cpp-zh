
### 6.1.2 Accessing Array Elements

Individual elements in an array values are accessed by an integer index i, using the notation values[i].

The values stored in an array are called its elements. Each element has a position number, called an index. To access a value in the values array, you must specify which index you want to use. That is done with the [] operator:

```
values[4] = 34.5;
```

Now the element with index 4 is filled with 34.5. (See Figure 2).

![](img/d61019b035dd82beb581604273c0ee6b_311_0.png)

Figure 2 Filling an Array Element

You can display the contents of the element with index 4 with the following command:

```
cout << values[4] << endl;
```

As you can see, the element values[4] can be used like any variable of type double.

An array element can be used like any variable.

In C++, array positions are counted in a way that you may find surprising. If you look carefully at Figure 2, you will find that the fifth element was filled when we changed values[4]. In C++, the elements of arrays are numbered starting at 0. That is,

- values[0], the first element
- values[1], the second element
- values[2], the third element
- values[3], the fourth element
- values[4], the fifth element
- ...
- values[9], the tenth element

You will see in Chapter 7 why this numbering scheme was chosen in C++.

You have to be careful about index values. Trying to access an element that does not exist in the array is a serious error. For example, if values has twenty elements, you are not allowed to access values[20].

An array index must be at least zero and less than the size of the array.

![](img/d61019b035dd82beb581604273c0ee6b_311_1.png)

Like a post office box that is identified by a box number, an array element is identified by an index.

## Computing & Society 6.1 Computer Viruses

![](img/d61019b035dd82beb581604273c0ee6b_314_0.png)

In November 1988, Robert Morris, a student at Cornell University, launched a so-called virus program that infected a significant fraction of computers connected to the Internet (which was much smaller then than it is now). Morris was sentenced to three years probation, 400 hours of community service, and a $10,000 fine.

In order to attack a computer, a virus has to find a way to get its instructions executed. This particular program carried out a "buffer overrun" attack, providing an unexpectedly large input to a program on another machine. That program allocated an array of 512 characters, under the assumption that nobody would ever provide such a long input. Unfortunately, that program was written in the C programming language. C, like C++, does not check that an array index is less than the length of the array. If you write into an array using an index that is too large, you simply overwrite memory locations that belong to some other objects. C programmers are supposed to provide safety checks, but that had not happened in the program under attack. The virus program purposefully filled the 512-character array with 536 bytes. The excess 24 bytes overwrote a return address, which the attacker knew was stored just after the array. When the function that read the input was finished, it didn't return to its caller but to code supplied by the virus (see the figure). The virus was thus able to execute its code on a remote machine and infect it.

In recent years, computer attacks have intensified and the motives have become more sinister. Instead of disabling computers, viruses often take permanent residence in the attacked computers. Criminal enterprises rent out the processing power of millions of hijacked computers for sending spam e-mail. Other viruses monitor every keystroke and send those that look like credit card numbers or banking passwords to their master, or encrypt all disk files and demand a monetary ransom payment from the unfortunate user to unlock the files.

Typically, a machine gets infected because a user executes code downloaded from the Internet, clicking on an icon or link that purports to lead to something interesting, such as a game or video clip. Antivirus programs check all downloaded programs against an ever-growing list of known viruses.

When you use a computer for managing your finances, you need to be aware of the risk of infection. If a virus reads your banking password and empties your account, you will have a hard time convincing your financial institution that it wasn't your act, and you will most likely lose your money. It is a good idea to use banks that require "two-factor authentication" for major transactions, such as a callback on your cell phone.

Viruses are even used for military purposes. In 2010, a virus dubbed Stuxnet spread through Microsoft Windows and infected USB sticks. The virus looked for Siemens industrial computers and reprogrammed them in subtle ways. It appears that the virus was designed to damage the centrifuges of the Iranian nuclear enrichment operation. The computers controlling the centrifuges were not connected to the Internet, but they were configured with USB sticks, some of which were infected. Security researchers believe that the virus was developed by U.S. and Israeli intelligence agencies, and that it was successful in slowing down the Iranian nuclear program. Neither country has officially acknowledged or denied their role in the attacks.

![](img/d61019b035dd82beb581604273c0ee6b_314_1.png)

## 6.2 Common Array Algorithms

In the following sections, we discuss some of the most common algorithms for processing sequences of values. We present the algorithms so that you can use them with fully and partially filled arrays as well as vectors (which we will introduce in Section 6.7). When we use the expression size of values, you should replace it with a constant or variable that yields the number of elements in the array (or the expression values.size() if values is a vector.)

### 6.2.1 Filling

This loop fills an array with zeroes:

```
for (int i = 0; i < size of values; i++)
{
    values[i] = 0;
}
```

Next, let us fill an array squares with the numbers 0, 1, 4, 9, 16, and so on. Note that the element with index 0 contains 0², the element with index 1 contains 1², and so on.

```
for (int i = 0; i < size of squares; i++)
{
    squares[i] = i * i;
}
```

### 6.2.2 Copying

Consider two arrays:

```
int squares[5] = { 0, 1, 4, 9, 16 };
int lucky_numbers[5];
```

Now suppose you want to copy all values from the first array to the second. The following assignment is an error:

```
lucky_numbers = squares; // Error
```

In C++, you cannot assign one array to another. Instead, you must use a loop to copy all elements:

```
for (int i = 0; i < 5; i++)
{
    lucky_numbers[i] = squares[i];
}
```

To copy an array, use a loop to copy its elements to a new array.

![](img/d61019b035dd82beb581604273c0ee6b_315_0.png)

Figure 4 Copying Elements to Copy an Array

### 6.2.3 Sum and Average Value

You have already encountered this algorithm in Section 4.7.1. Here is the code for computing the sum of all elements in an array:

```
double total = 0;
for (int i = 0; i < size of values; i++)
{
    total = total + values[i];
}
```

### 6.2.7 Linear Search

You often need to search for the position of an element so that you can replace or remove it. Visit all elements until you have found a match or you have come to the end of the array. Here we search for the position of the first element equal to 100.

> A linear search inspects elements in sequence until a match is found.

![](img/d61019b035dd82beb581604273c0ee6b_317_0.png)

© yekorah/Getty Images.

> To search for a specific element, visit the elements and stop when you encounter the match.

```
int pos = 0;
bool found = false;
while (pos < size of values && !found)
{
    if (values[pos] == 100)
    {
        found = true;
    }
    else
    {
        pos++;
    }
}
```

If found is true, then pos is the position of the first match.

### 6.2.8 Removing an Element

Consider a partially filled array values whose current size is stored in the variable current_size. Suppose you want to remove the element with index pos from values. If the elements are not in any particular order, that task is easy to accomplish. Simply overwrite the element to be removed with the last element, then decrement the variable tracking the size. (See Figure 5.)

```
values[pos] = values[current_size - 1];
current_size--;
```

The situation is more complex if the order of the elements matters. Then you must move all elements following the element to be removed to a lower index, then decrement the variable holding the size of the array. (See Figure 6.)

```
for (int i = pos + 1; i < current_size; i++)
{
    values[i - 1] = values[i];
}
current_size--;
```

![](img/d61019b035dd82beb581604273c0ee6b_317_1.png)

![](img/d61019b035dd82beb581604273c0ee6b_317_2.png)
