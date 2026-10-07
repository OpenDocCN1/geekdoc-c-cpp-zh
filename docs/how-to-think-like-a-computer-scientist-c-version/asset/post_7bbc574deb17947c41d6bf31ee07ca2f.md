
## Chapter 7
## Strings and things

## 7.1 Containers for strings

We have seen five types of values—booleans, characters, integers, floating-point numbers and strings—but only four types of variables—bool, char, int and double. So far we have no way to store a string in a variable for or perform operations on strings.

In fact, there are several kinds of variables in C++ that can store strings. One is a basic type that is part of the C++ language, sometimes called a “native string.” The syntax for C strings is a bit ugly, and using them requires some concepts we have not covered yet, so for the most part we are going to avoid them.

The string type we are going to use is an `apstring`, which is a type created specifically for the Computer Science AP Exam.

Unfortunately, it is not possible to avoid C strings altogether. In this chapter I will warn you about some problems you might run into using `apstring`s instead of C strings.

> In order for me to talk about AP classes in this book, I have to include the following text: Inclusion of the C++ classes defined for use in the Advanced Placement Science courses does not constitute endorsement of the other material in this textbook by the College Board, Educational Testing service, or the Computer Science Development Committee. The versions of the C++ classes defined in the AP Computer Science courses included in this textbook were accurate as of 20 July 1999. Revisions to the classes may have been made since that.

You might be wondering what they mean by class. It will be a few more chapters before I can give a complete definition, but for now a class is a collection of functions that defines the operations we can perform on some type. The `apstring` class contains all the functions that apply to `apstrings`.

## 7.2 apstring variables

You can create a variable with type `apstring` in the usual ways:

```
apstring first;
first = "Hello";
apstring second = "world";
```

The first line creates an `apstring` without giving it a value. The second line assigns it the string value "Hello". The third line is a combined declaration and assignment, also called an initialization.

Normally when string values like "Hello", or "world" appear, they are treated as C strings. In this case, when we assign them to an `apstring` variable, they are converted automatically to `apstring` values.

We can output strings in the usual way:

```
cout << first << second << endl;
```

In order to compile this code, you will have to include the header file for the `apstring` class, and you will have to add the file `apstring.cpp` to the list of files you want to compile. The details of how to do this depend on your programming environment.

Before proceeding, you should type the program above and make sure you can compile and run it.

## 7.3 Extracting characters from a string

Strings are called "strings" because they are made up of a sequence, or string, of characters. The first operation we are performing on a string is to extract one of the characters. C++ uses square brackets ([ and ]) for this operation:

```
apstring fruit = "banana";
char letter = fruit[1];
cout << letter << endl;
```

The expression `fruit[1]` indicates that I get the character number 1 from the string named fruit. The result is stored in a char named letter. When you output the value of letter, I get a surprise:

a

a is not the first letter of "banana". Unless you are a computer scientist. For perverse reasons, computer scientists always start counting from zero. The 0th letter ("zeroth") of "banana" is b. The 1st letter ("oneth") is a and the 2nd ("twoeth") is n.

If you want the zeroth letter of the string, you have to put zero in the square brackets:

```
char letter = fruit[0];
```

## 7.4 Length

To find the length of a string (number of characters), we can use the length function. The syntax for calling this function is a little different from what we've seen before:

```
int length;
length = fruit.length();
```

To describe this function call, we would say that we are invoking the length function on the string named fruit. This vocabulary may seem strange, but we will see many more examples where we invoke a function on an object. The syntax for function invocation is called "dot notation", because the dot (period) separates the name of the object, fruit, from the name of the function, length. `length()` takes no arguments, as indicated by the empty parentheses (). The return value is an integer, in this case 6. Notice that it is legal to have a variable with the same name as a function.

To find the last letter of a string, you might be tempted to try something like

```
int length = fruit.length();
char last = fruit[length]; // WRONG!
```

That won't work. The reason is that there is no 6th letter in "banana". Since we started counting at 0, the 6 letters are numbered from 0 to 5. To get the last character, you must subtract 1 from length.

```
int length = fruit.length();
char last = fruit[length-1];
```

## 7.5 Traversal

A common thing to do with a string is start at the beginning, select each character in turn, do something to it, and continue until the end. This pattern of processing is called traversal. A natural way to traverse is:

```
int index = 0;
while (index < fruit.length()) {
  char letter = fruit[index];
  cout << letter << endl;
  index = index + 1;
}
```

This loop traverses the string and outputs each letter.

## 7.6 A run-time error

Way back in Section 1.3 I talked about run-time errors, which are errors that cause the program to crash. If you use an index that is negative or greater than length-1, you will get a run-time error and a message like this:

```
apstring fruit = "banana";
cout << fruit[6];
```

## 7.7 The find function

The `apstring` class provides other functions that you can invoke on strings. Instead of taking an index and extracting the character at that index, `find` takes a character and returns the index where it appears. According to the documentation, it returns the index of the first appearance. If the given letter does not appear in the string, it returns -1.

```
apstring fruit = "banana";
int index = fruit.find('a');
```

In addition, there is a version of `find` that takes another `apstring` as an argument and finds the index where the substring appears in the string. For example:

```
apstring fruit = "banana";
int index = fruit.find("nan");
```

## 7.8 Our own version of find

If we are looking for a letter in an apstring, we may not want to start at the beginning of the string. One way to generalize the find function is to write a version that takes an additional parameter--the index where we should start. Here is an implementation:

```
int find(apstring s, char c, int i)
{
  while (i<s.length()) {
    if (s[i] == c) return i;
    i = i + 1;
  }
  return -1;
}
```

## 7.9 Looping and counting

The following program counts the number of times the letter 'a' appears in a string:

```
apstring fruit = "banana";
int length = fruit.length();
int count = 0;

int index = 0;
while (index < length) {
  if (fruit[index] == 'a') {
    count = count + 1;
  }
  index = index + 1;
}
cout << count << endl;
```

This program demonstrates a common idiom, called a counter. The variable count is initialized to zero then incremented each time we find an 'a'.
