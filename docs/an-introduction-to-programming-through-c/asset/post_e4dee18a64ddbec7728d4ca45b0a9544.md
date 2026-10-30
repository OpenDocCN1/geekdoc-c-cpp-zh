
## 14.1 Character strings

An array of characters can be defined just as you define arrays of doubles or ints.

```
char name[20], residence[50];
```

The above defines two arrays, name and residence of lengths 20 and 50, ostensibly for storing the name and the residence. Since we will usually not know the exact number of characters in a name or in an address, it is customary to define arrays of what we guess might be the largest possible length. This might seem wasteful, and it is, and we will see better alternatives in later chapters.

So if we want to store a character string “Shivaji” in the array, we will be storing ‘S’ in name[0], ‘h’ in name[1] and so on. The string is 7 characters long, and you would think that we should store this length somewhere. While printing the string for example, we clearly do not want the name[7] through name[19] printed. The convention used in the C language, and inherited into C++ from there, is that instead of storing the length explicitly, we store a special character at the end of the actual string. The special character used is the one with ASCII value 0, and this can be written as ‘\0’. Note that ‘\0’ is not printable, and is not expected to be a part of any real text string. So it unambiguously marks the end of the string.

Special constructs are provided for initializing character arrays. So indeed we may write

```
char name[20] = "Shivaji";
char residence[50] = "Main Palace, Raigad";
```

The character string “Shivaji” has 7 characters. So these will be placed in the first 7 elements of name. The eighth element, name[7] will be set to ‘\0’. Similarly only 20 elements of residence will be initialized, including the last ‘\0’. Note by the way that capital and small letters have different codes.

Here is an alternative form.

```
char name[] = "Shivaji";
char residence[] = "Main Palace, Raigad";
```

In this, C++ will calculate the lengths of name and residence. Following the previous discussion, these will be set to 8 and 20 respectively.

We can manipulate strings stored in char arrays by going over the elements in a for loop, for example.

### 14.1.1 Output

Printing out the contents of a character array is simple. Assuming name is a character array as before,

```
cout << name;
```

would cause the contents of name from the beginning to the '\0' character to be printed on the screen.

The general form of the above statement is:

```
cout << charptr;
```

where charptr is an expression which evaluates to a pointer to a char type. If name is a character array, then name indeed is of type pointer to char. This statement causes characters starting from the address charptr to be printed, until a '\0' character is encountered. Thus character arrays passed to functions can be printed in the expected manner.

### 14.1.2 Input

To read in a string into a char array you may use the analogous form:

```
cin >> charptr;
```

Here charptr could be the name of a char array, or more generally, an expression of type pointer to char. The statement will cause a whitespace delimited string typed by the user to be read into the memory starting at the address denoted by charptr. After storing the string the '\0' character will be stored. Here is an example.

```
char name[20];
cout << "Please type your name: ";
cin >> name;
```

The second statement asks you to type your name and the third, cin >> name; reads in what you type into the array name. The following points are worth noting:

- 1. From what you type, the initial whitespace characters will be ignored. The character string starting with the first non-whitespace character and ending just before the following whitespace character will be taken and placed in name. Thus if I type
Abhiram Ranade
with some leading whitespace, the leading whitespace will be dropped and only "Abhiram" would go into name. Next, following "Abhiram" a null character, i.e. '\0' would be stored. Thus the letters 'A' through 'm' would go into name[0] through name[6], and name[7] would be set to '\0'. Note that all this is very convenient in that the a single statement reads in all the characters, and further the '\0' is also automatically placed after the last character read in.
- 2. This way of reading in text is not useful if the text contains spaces. Thus in the above example, "Ranade" would not be read in into name. For that it is necessary to use the getline command discussed below.
- 3. This statement is potentially unsafe. In the above example if the user had typed in more than 20 characters without a whitespace in between, all those would be stored starting at name[0]. Thus the characters read in would be stored past the end of the designated array name, possibly writing into memory that might have been allocated for some other variable.

The safe alternative to this is to use the following command.

```
cin.getline(x,n);
```

where x must be a name of a char array, or more generally a pointer to char, and n an integer. This will cause whatever the user types, including whitespace characters, to be placed starting from the address x, until one of the following occurs

- A newline character is typed¹ by the user. In this case all characters upto the newline are copied into memory starting from the address x. The newline character is not copied. It is discarded.
- n-1 characters are typed without a newline. In this case all the characters are placed into memory starting from address x, followed by a '\0' character.

As you may guess, it is customary to use the length of x as the argument n. So for example we can write:

```
char name[20];
 cin.getline(name,20);
```

In this case at most 19 characters that the user types will be copied, and we will have no danger of overflowing past the array limit.

### 14.1.3 Character array processing

Character arrays behave like ordinary integer arrays, except when it comes to reading and printing, and in that they contain a '\0' character which marks the end of the useful portion of the array. So processing them is reasonably straight forward. Note that characters are a subtype of integers, and as such we can perform arithmetic on characters, and compare them, just as we do for integers.

Our first example is a function for determining the length of the text stored in a char array.

```
int length(char *txt){
    //precondition: txt points to sequence of '\0' terminated characters.
    int L=0;
    while(txt[L] != '\0') L++;
    return L;
}
```

The function takes a single argument, say the array name (or the pointer to the zeroth element of the array). Notice that the actual length of the array is not needed. This is because we access elements only till the null character. Indeed, the function simply steps through the elements of the array, and returns the index at which it finds the null character, '\0'. Since the starting index is 0, the null character will be at index equal to the length of the text string.

Our second example is a function for copying a string stored in an array source to another array destination. This is like copying other arrays, except that we must only worry about the useful portion of the source array, i.e. till the occurrence of the '\0' character. The function does not worry at all about the lengths of the 2 arrays as defined, it is assumed that the call has been made ensuring that indices will not exceed the array bounds.

```
```c
void scopy(char destination[], char source[])
// precondition: '\0' must occur in source.  destination must be long
// enough to hold the entire source string + '\0'.
{
    int i;
    for(i=0; source[i] != '\0'; i++)
        destination[i]=source[i];
    destination[i]=source[i];    // copy the '\0' itself
}
```
```

As an example of using this, note that a string constant can be used any place a pointer to char is needed. Thus we can write scopy(name,"Einstein") which would simply set the name to “Einstein”.

Here is a more interesting function: it takes two strings and returns which one is lexicographically smaller, i.e. would appear first in the dictionary. The function simply compares corresponding characters of the two strings, starting at the 0th. If the end of the strings is reached without finding unequal characters, then it means that the two strings are identical, in which case we must return ‘=’. If at some comparison we find the character in one string to be smaller than the other, that string is declared smaller. If one string ends earlier, while the preceding characters are the same, then the string that ends is smaller.

This logic is implemented in the code below. We maintain the loop invariant: characters 0 through i-1 of both arrays must be non null and identical. So if we find both a[i] and b[i] to be null, clearly the strings are identical and hence we return '='. If a[i] is null but not b[i], then a is a prefix of b. Because prefixes appear before longer strings in the dictionary, we return '<'. We proceed similarly if b[i] is null but not a[i]. If a[i]>b[i] we return '>', if a[i]<b[i] we return '<'. If none of these conditions apply, then the ith character in both strings must be non-null and identical. So the invariant for the next iteration is satisfied. So we increment i and go to the next iteration.

```
```c
char compare(char a[], char b[])
// returns '<' if a is smaller, '=' if equal, '>' if b is smaller.
{
    int i = 0;
    while(true){                    // Invariant: a[0..i-1] == b[0..i-1]
        if(a[i] == '\0' && b[i] == '\0') return '=';
        if(a[i] == '\0') return '<';
        if(b[i] == '\0') return '>';
        if(a[i]<b[i]) return '<';
        if(a[i]>b[i]) return '>';
        i++;
    }
}
```
```
