
## Arrays of Characters

An array of elements of type char can have a dual personality. It can simply be an array of characters, in which each element stores one character, or it can represent a string. In the latter case, the characters in the string are stored in successive array elements, followed by a special string termination character called the null character that you write as '\0'. The null character marks the end of the string.

A character array that is terminated by '\0' is referred to as a C-style string. This contrasts with the string type from the Standard Library that we'll explain in detail in Chapter 7. Objects of type string are much more flexible and convenient for string manipulation than using arrays of type char. For the moment, we'll introduce C-style strings in the context of arrays in general and return to them and to type string in detail in Chapter 7.

You can define and initialize an array of elements of type char like this:

```cpp
char vowels[5] {'a', 'e', 'i', 'o', 'u'};
```

This isn't a string—it's just an array of five characters. Each array element is initialized with the corresponding character from the initializer list. As with numeric arrays, if you provide fewer initializing values than there are array elements, the elements that don't have explicit initial values will be initialized with the equivalent of zero, which is the null character, '\0' in this case. This means that if there are insufficient initial values, the array will effectively contain a string. Here's an example:

```cpp
char vowels[6] {'a', 'e', 'i', 'o', 'u'};
```

The last element will be initialized with '\0'. The presence of the null character means that this can be treated as a C-style string. Of course, you can still regard it as an array of characters.

You could leave it to the compiler to set the size of the array to the number of initializing values:

```cpp
char vowels[] {'a', 'e', 'i', 'o', 'u'};    // An array with five elements
```

This also defines an array of five characters initialized with the vowels in the braced initializer. You can also declare an array of type char and initialize it with a string literal, as follows:

```cpp
char name[10] {"Mae West"};
```

This creates a C-style string. Because you're initializing the array with a string literal, the null character will be stored in the element following the last string character, so the contents of the array will be as shown in Figure 5-5.

![](img/020c376b6cc4874983a4344f51a256de_163_0.png)

*Figure 5-5. An array of elements of type char initialized with a string literal*

You can leave the compiler to set the size of the array when you initialize it with a string literal:

```cpp
char name[] {"Mae West"};
```

This time, the array will have nine elements: eight to store the characters in the string, plus an extra element to store the string termination character. Of course, you could have used this approach when you declared the vowels array:

```cpp
char vowels[] {"aeiou"};      // An array with six elements
```

There’s a significant difference between this and the previous definition for vowels without an explicit array dimension. Here you’re initializing the array with a string literal. This has '\0' appended to it implicitly to mark the end of the string, so the vowels array will contain six elements. The array created with the earlier definition will have only five elements and can’t be used as a string.

You can output a string stored in an array just by using the array name. The string in the name array, for example, could be written to cout with this statement:

```cpp
std::cout << name << std::endl;
```

This will display the entire string of characters, up to the '\0'. There must be a '\0' at the end. If there isn't, the standard output stream will continue to output characters from successive memory locations, which almost certainly contain garbage, until either a null character happens to turn up or an illegal memory access occurs.

> **Caution** You can't output the contents of an array of a numeric type by just using the array name. This works only for char arrays. And even a char array passed to an output stream must be terminated with a null character or the program will likely crash.

This example analyzes an array of elements of type char to work out how many vowels and consonants are used in it:

```cpp
// Ex5_10.cpp
// Classifying the letters in a C-style string
import <iostream>;
#include <cctype>

int main()
{
  const int max_length {100};   // Array size
  char text[max_length] {};     // Array to hold input string

  std::cout << "Enter a line of text:" << std::endl;

  // Read a line of characters including spaces
  std::cin.getline(text, max_length);
  std::cout << "You entered:\n" << text << std::endl;

  size_t vowels {};            // Count of vowels
  size_t consonants {};        // Count of consonants
```

This would allow multiple lines of text to be entered because the `\n` that results from pressing Enter would no longer terminate the input operation. Of course, the total number of characters that you can enter in the read operation is still limited by `max_length`.

Just to show what you can do, the program outputs the string that was entered using just the array name, `text`. The text string is then analyzed in a straightforward manner in the `for` loop. The second control expression within the loop will be false when the character at the current index, `i`, is the null character, so the loop ends when the null character is reached.

Next, to work out the number of vowels and consonants, you only need to inspect alphabetic characters, and the `if` statement selects them; `isalpha()` only returns true for alphabetic characters. Thus, the switch statement executes only for letters. Converting the switch expression to lowercase avoids having to write cases for uppercase as well as lowercase letters. Any vowel will select the first case, and the default case is selected by anything that isn't a vowel, which must be a consonant, of course.

By the way, because the null character `\0` is the only character that converts to the Boolean false (analogous to 0 for integral values), you could write the `for` loop in Ex5_10 like this as well:

```cpp
for (int i {}; text[i]; i++)
{
    ...
}
```

## Multidimensional Arrays

All the arrays so far have required a single index value to select an element. Such an array is called a *one-dimensional array* because varying one index can reference all the elements. You can also define arrays that require two or more index values to access an element. These are referred to generally as *multidimensional arrays*. An array that requires two index values to reference an element is called a *two-dimensional array*. An array requiring three index values is a *three-dimensional array*, and so on, for as many dimensions as you think you can handle.

Suppose, as an avid gardener, that you want to record the weights of the carrots you grow in your small vegetable garden. To store the weight of each carrot, which you planted in three rows of four, you could define a two-dimensional array:

```cpp
double carrots[3][4] {};
```

This defines an array with three rows of four elements and initializes all elements to zero. To reference a particular element in the array, you need two index values. The first index specifies the row, from 0 to 2, and the second index specifies a particular carrot in that row, from 0 to 3. To store the weight of the third carrot in the second row, you could write the following:

```cpp
carrots[1][2] = 1.5;
```

Figure 5-6 shows the arrangement of this array in memory. The rows are stored contiguously in memory. As you can see, the two-dimensional array is effectively a one-dimensional array of three elements, each of which is a one-dimensional array with four elements. You have an array of three arrays that each has four elements of type double. Figure 5-6 also indicates that you can use the array name plus a single index value between square brackets to refer to an entire row.
