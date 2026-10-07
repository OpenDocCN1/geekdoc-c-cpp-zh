# Introducing the string Class

The main difference between string objects and character arrays shown in Listing 4.7 is that you declare a string object as a simple variable, not as an array:

```
string str1; // create an empty string object
string str2 = "panther"; // create an initialized string
```

The class design allows the program to handle the sizing automatically. For instance, the declaration of str1 creates a string object of length zero, but the program automatically resizes str1 when it reads into str1:

```
cin >> str1; // str1 resized to fit input
```

This makes using a string object more convenient and safer than using an array. Conceptually, one thinks of an array as a collection of char storage units used to store a string but of a string class as a single entity representing the string.

# C++11 String Initialization

As you might expect by now, C++11 enables list-initialization for C-style strings and string objects:

```
char first_date[] = {\Le Chadon Dudu";
char second_date[] = {\The Elephant Plate";
string third_date = {\The Bread Bowl";
string fourth_date = {\Hank's Fine Eats"};
```

# Assignment, Concatenation, and Appending

The string class makes some operations simpler than is the case for arrays. For example, you can't simply assign one array to another. But you can assign string object to another:

```
char char1[20]; // create an empty array
char char2[20] = "jaguar"; // create an initialized array
string str1; // create an empty string object
string str2 = "panther"; // create an initialized string
char1 = char2; // INVALID, no array assignment
str1 = str2; // VALID, object assignment ok
```

The class simplifies combining strings. You can use the + operator to add two string objects together and the += operator to add a string to the end of an existing string. Continuing with the preceding code, we have the following possibilities:

```
string str3;
str3 = str1 + str2; // assign str3 the joined strings
str1 += str2; // add str2 to the end of str1
```

Listing 4.8 illustrates these uses. Note that you can add and append C-style strings as well as string objects to a string object.