
[content]
188 Learning SAS by Example: A Programmer's Guide, Second Edition

One of these modifiers (k) reverses the action of the COMPRESS function (to help remember, k is to keep). When you use the k modifier, the COMPRESS function keeps the selected characters and removes everything else.

> Note: This is one of the most useful ways to use the COMPRESS function. It is usually better to specify the characters you wish to keep rather than the ones you want to remove.

This table shows some of the most useful modifiers.

| Modifier | Action |
|---|---|
| d | Adds numbers (digits) to the list of characters to be deleted |
| a | Adds upper- and lowercase letters to the list of characters to be deleted |
| i | Ignores case |
| k | Keeps listed characters without removing them |
| s | Adds blanks, tabs, line-feeds, or carriage returns to the list of characters to be deleted |
| p | Adds punctuation to the list of characters to be deleted |

Here are a few examples: If String = "Xy2Z3",

| Function | Description | Value |
|---|---|---|
| compress(String, 'a') | Removes all letters | 123 |
| compress(String, 'kd') | Keeps digits (deletes everything else) | 123 |
| compress(String, 'wxyz', 'i') | Removes wxyz and ignores case | 123 |
| compress("AB C99", 'pd') | Removes punctuation and digits | AB C |

Notice that if you want to use modifiers and do not specify a second argument, you need to use two commas to indicate that the modifiers are the third argument.

Here is Program 12.6 using modifiers:

## Program 12.7: Demonstrating the COMPRESS Modifiers

```
data Phone;
  length PhoneNumber $ 10;
  set Learn.Phone;
  PhoneNumber = compress(Phone,'kd');
  *Keep only digits;
run;
```

The resulting data set is identical to the one listed previously.

As you can see in this example, it is easier to use the k modifier to indicate what you want to keep, than it is to list all of the characters you want to remove.

## 12.8 Searching for Characters

There are a large number of SAS functions that allow you to search for individual characters or character substrings.

Let's start with a problem where you are given a SAS data set containing measurements in either English or metric units.

First, here is a listing of data set Mixed_Units:

Figure 12.8: Listing of Mixed_Units

![](img/e9e15d853989558188e1c83b0ae655b0_200_0.png)

The units are not consistently in upper- or lowercase, there may be or not be a period in the units, and they vary slightly. This looks like a difficult problem—but not when you have SAS character functions.

Problems of this type are quite common. Take a look at the program below and then we will discuss the approach:

## Program 12.8: Demonstrating the COMPRESS and FIND Functions

```
data Metric;
set Learn.Mixed_Units;
Wt_Kg = input(compress(Weight,'kd'),12);
if find(Weight,'lb','i') then Wt_Kg = Wt_Kg/2.2;
Ht_Cm = input(compress(Height,'kd'),12);
if find(Height,'in','i') then Ht_Cm = Ht_Cm*2.54;
```

The COMPRESS function extracts the digits from the character value. Even though you called this variable Wt_Kg, you don't know at this point whether or not the weight you read was in pounds or kilograms.

Next, you use the FIND function to search the value of Weight for the characters 1b. Here's how this function works:

In its simplest form, you supply the FIND function with two arguments, like this:

```
find(string, find_string)
```

Here, string is the string you want to search and find_string is the string you are looking for. If find_string is not found, the function returns a zero. For example, the value of the following statement:

Learning SAS by Example: A Programmer's Guide, Second Edition

find("what hat is that","hat")
returns a value of 2, the position where the string hat begins. An older function, INDEX, was similar to the FIND function as described here. However, the FIND function has added capabilities; you can add two arguments to the FIND function. One of these arguments is a modifier that alters how the search starts. The most useful modifier is the i (ignore case) modifier. You can also specify a starting position at where to start the search. If you use a negative value, the search proceeds from left to right. To summarize, the FIND function has the following syntax:

```
find(string, find-string, modifiers, starting-position)
```

By the way you can use modifiers, a starting position, or both, and they can be in any order! How is that possible? Because modifiers are always character values and starting positions are always a numeric value, SAS can figure out which argument is a modifier and which is a starting position.
In the previous program, the i modifier is used so that the search looks for upper- or lowercase values of LB or IN.

If you determine the units of Weight using the characters 'LB' (in upper- or lowercase), you divide the value of Wt_Kg by 2.2 to convert pounds to kilograms. If you determine the units of Height using the characters 'IN' (in upper- or lowercase), you multiply the value of Ht_Cm by 2.54 to convert centimeters. This looks like a difficult problem—but not when you have SAS character functions.

Figure 12.9: Listing of Data Set

| Weight | Height | Wt_Kg | Ht_Cm |
|---|---|---|---|
| 100lb | 70in | 45.45 | 177.8 |
| 150lb | 65in | 68.18 | 165.1 |
| 200lb | 72in | 90.91 | 182.9 |
| 250lb | 68in | 113.64 | 172.7 |

The units are not consistently in upper- or lowercase, there may be or not be a period in the units, and they vary slightly. This looks like a difficult problem—but not when you have SAS character functions.

Problems of this type are quite common. Take a look at the program below and then we will discuss the approach:

Chapter 12: Working with Character Functions

## 12.9 Searching for Individual Characters

A companion function to FIND is FINDC. While FIND searches a string for a specific substring, FINDC searches a string for any one of characters.

| Line | Function | Value Returned |
|---|---|---|
| 1 | find('XYZBA', 'ABC') | 0 |
| 2 | findc('XYZBA', 'ABC') | 4 |
| 3 | findc('ABCDE', 'D') | 4 |
| 4 | findc('ABCDE', 'D') | 4 |
| 5 | findc('XYZba', 'ABC', 'i') | 0 |
| 6 | findc('XYZba', 'ABC', 'i') | 4 |

In Line 1 of the table, you are looking for the string ABC. Because this string does not appear in the argument, the function returns 0. In line 2, the FINDC function returns 4 (the position of C). When you are looking for a single character, as in Lines 3 and 4, functions return the same value. The last two lines in the table demonstrate the i (ignore case) modifier that you can use with these.

## 12.10 Searching for Words in a String

The FINDW is similar to the FIND function, except that it searches for words (hence the W in the function name).

Words are defined as a series of characters that start and end with a word boundary. The default word boundaries are the beginning of a string, an end of a string, a blank, and the following: $%&*()+-/. The list of delimiters is slightly different if you are using the EBCDIC character set. You can specify alternate delimiters as the third argument (you might want to use a single blank of the default list of characters).

The syntax for this function is as follows:

```
findw(string, delimiters, modifiers, starting-position)
```

Here, string is the string you want to search, find-string is the string you are looking for, and delimiters supplies a list of word delimiters. Note that if you want to supply modifiers (most likely the i ignore case modifier), you must also supply one or more delimiters (even if all you want to use the default values).

The following table shows the difference between the two functions, FIND and FINDW.

| Function | Value Returned |
| find('there is the dog', 'the') | 1 (position of the string) |
| findw('there is the dog', 'the') | 10 (start of the word the) |
| findw('there is THE dog','the',' 'i') | 10 (Start of the THE) |
| findw('pear:apple','apple',':') | 6 (start of the word apple) |

