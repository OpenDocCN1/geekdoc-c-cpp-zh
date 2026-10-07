
[content]
increment is to increase by one; it is the opposite of decrement, and unrelated to decrement, which is a noun.) When we exit the loop, count contains the result: the total number of a's.

As an exercise, encapsulate this code in a function named countLetters, and generalize it that it accepts the string and the letter as arguments.

As a second exercise, rewrite this function that instead of traversing the string, it uses the version of find we wrote in the previous section.

## 7.10 Increment and decrement operators

Incrementing and decrementing are such common operations that C++ provides special operators for them. The ++ operator adds one to the current value of an int, char and -- subtracts one. Neither operator works on apstrings, and neither should be used on bools.

Technically, it is legal to increment a variable and use it in an expression at the same time. For example, you might see something like:

```cpp
cout << i << endl;
```

Looking at this, it is not clear the increment will take effect before or after the value is displayed. Because expressions like this tend to be confusing, I discourage you from using them. In fact, to discourage you even more, I'm not going to tell you what the result is. If you really want to know, you can try.

Using the increment operators, we can rewrite the letter-counter:

```cpp
int index = 0;
while (index < length) {
  if (fruit[index] == 'a') {
    count++;
  }
  index++;
}
```

It is a common error to write something like

```cpp
index = index++; // WRONG!
```

Unfortunately, this is syntactically legal, so the compiler will not warn you. The effect of this statement is to leave the value of index unchanged. This is often a big bug to track down.

Remember, you can write index = index+1; or you can write index++; but you shouldn't mix them.

## 7.11 String concatenation

Interestingly, the + operator can be used on strings; it performs concatenation. To concatenate means to join the operands end to end. For example:

```cpp
apstring fruit = "banana";
apstring bakedGood = "put bread";
apstring dessert = fruit + bakedGood;
cout << endl;
```

The output of this program is banana nut bread.
unfortunately, the + operator does not work on native C strings, so you cannot write something like

```cpp
apstring dessert = "banana" + " nut bread";
```

because both operands are C strings. As long as one of the operands is an apstring, C++ will automatically convert the other.
It is also possible to concatenate a character onto the beginning or end of an apstring. In the following example, we will use concatenation and character arithmetic to output an abecedarian series.

"Abecedarian" refers to a series or list in which the elements appear in alphabetical order. For example, in Robert McCloskey's book Make Way for Ducklings, the names of the ducklings are Jack, Kack, Lack, Mack, Nack, Onack, Pack and Quack. Here is a list that outputs these names in order:

```cpp
apstring suffix = "ack";

char letter = 'J';
while (letter <= 'Q') {
  cout << letter + suffix << endl;
  letter++;
}
```

The output of this program is:

- Jack
- Kack
- Lack
- Mack
- Nack
- Oack
- Pack
- Quack

Of course, that's not quite right because I've misspelled "Ouack" and "Quack."
As an exercise, modify the program to correct this error.

Again, be careful to use string concatenation only with apstrings and not in native C strings. Unfortunately, an expression like letter + "ack" is syntactically legal in C++, although it produces a very strange result, at least in my development environment.

## 7.12 apstrings are mutable

You can change the letters in an apstring one at a time using the [] operator in the left side of an assignment. For example,

```cpp
apstring greeting = "Hello, world!";
greeting[0] = 'J';
cout << greeting << endl;
```

produces the output Jello, world.

## 7.13 apstrings are comparable

All the comparison operators that work on ints and doubles also work on apstrings. For example, if you want to know if two strings are equal:

```cpp
if (word == "banana") {
  cout << "Yes, we have no bananas!" << endl;
}
```

The other comparison operations are useful for putting words in alphabetical order.

```cpp
if (word < "banana") {
  cout << " " << word << " comes before banana." << endl;
} else if (word > "banana") {
  cout << "Your word, " << word << " comes after banana." << endl;
} else {
  cout << "Yes, we have no bananas!" << endl;
}
```

You should be aware, though, that the apstring class does not handle upper lower cases the same way that people do. All the upper case letters come before the lower case letters. As a result, Your word, Zebra, comes before banana.

A common way to address this problem is to convert strings to a standard format, with all lower-case, before performing the comparison. The next sections explains how. I will not address the more difficult problem, which is making the program realize that zebras are not fruit.

## 7.14 Character classification

It is often useful to examine a character and test whether it is upper or lower case, or whether it is a character or a digit. C++ provides a library of functions that perform this kind of classification. In order to use these functions, you have to include the header file ctype.h.

```cpp
char letter = 'a';
if (isalpha(letter)) {
  cout << "The character " << letter << "" << endl;
}
```

You might expect the return value from isalpha to be a bool, but for reasons I don't want to think about it, it is actually an integer that is 0 if the argument is not a letter, and non-zero value if it is.

This oddity is not inconvenient as it seems, because it is legal to use this kind of integer in a conditional, as all non-zero values are treated as true. The value 0 is treated as false.

Technically, this sort of thing should not be allowed—integers are not.
