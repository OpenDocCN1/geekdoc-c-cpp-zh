
## Chapter 12: Working with Character Functions

Here is a program to merge the two data sets:

### Program 12.2: Changing Values to Uppercase

```sas
data Mixed;
  set Learn.Mixed;
  Name = upcase(Name);
run;

data Both;
  merge Mixed.Learn;
  by Name;
run;
```

As you might expect, the UPCASE function converts all letters to uppercase.

There are two functions, LOWCASE and PROPCASE, that convert letters to lowercase and proper, respectively. Proper case capitalizes the first letter of every "word" and converts the remaining letters to lowercase. By word, we mean any sequences separated by a delimiter. Default delimiters are blank, forward slash, hyphen, or parenthesis, and tab. You can specify delimiters as an optional second argument to the PROPCASE function if you want. Program 12.3 demonstrates the use of the PROPCASE function along with the COMPBL function described in the next section.

## 12.4 Removing Characters from Strings

The functions in this category are COMPBL and COMPRESS. The former converts two or more blanks to a single blank; the latter removes blanks (default action) or characters that you specify from a character value.

We demonstrate the COMPBL function (don't try to pronounce COMPBL; you might hurt yourself—just compress blanks) in a program to help standardize some addresses. In the listing below, notice that several of the lines contain multiple blanks and there is inconsistent with case as well.

### Figure 12.2: Listing of Data Set Address

| Name | Street | City | State | Zip |
|---|---|---|---|---|
| ron coDY | 1178 HIGH 480 | camp verde | tx | 78010 |
| jason Tran | 123 lake view drive | East Rockaway | ny | 11518 |

Note: This is a mono-spaced listing so that you can see multiple blanks.

Here is a program that converts multiple blanks to a single blank; converts the case for Name, and City to proper case; and converts the state abbreviations to uppercase:

### Program 12.3: Converting Multiple Blanks to a Single Blank and Demonstrating the PROPCASE Function

```sas
data Standard;
  set Learn.Address;
  Name = compbl(propcase(Name));
  Street = compbl(propcase(Street));
  City = compbl(propcase(City));
  State = upcase(State);
run;
```

Notice in this how you can nest one function within another. The COMPBL function has as its argument the value returned by the PROPCASE function (in this example, the order doesn't matter). The following listing shows the result:

### Figure 12.3: Listing of Data Set Standard

| Name | Street | City | State | Zip |
|---|---|---|---|---|
| Ron Cody | 1178 Highway 480 | Camp Verde | TX | 78010 |
| Jason Tran | 123 Lake View Drive | East Rockaway | NY | 11518 |

## 12.5 Joining Two or More Strings Together

Putting strings together is called concatenation. For example, if you have separate variables representing a first and last name, you can concatenate them (with a blank in between) to create a variable containing the full name.

The concatenation operator, || (or |||), has always been available to SAS programmers. For example, if One = ABC and Two = DEF, then One is equal to ABCDEF.

When you use the || operator, if you do not define the length of the resulting string beforehand, the length of this string is the sum of the lengths of the individual strings you are concatenating.

Three useful functions, CAT, CATS, and CATX, make this process much easier. The CAT function takes two or more arguments and concatenates them. It is almost the same as using the || operator, except the length of the resulting string defaults to the sum of the lengths of the arguments. The CATS function strips off leading and trailing blanks (remember S). The CATX function is similar to the CAT function, except you supply a separator as the first argument. When you use this function to concatenate strings, leading and trailing blanks are removed and the separator value is placed between each string.

### Program 12.4: Demonstrating Concatenation Functions

```sas
title "Concatenation Functions";
data _;
  length Name4 $15;
  First = 'Ron';
  Last = 'Cody';
  Join = ':' || First;
  Name1 = First || Last;
  Name2 = cat(First,Last);
  Name3 = catx(',',First,Last);
  put Join=/nName1=/nName2=/nName3=/nName4=;
run;
```

The first output, and then an explanation:

### Figure 12.4: Output from Program 12.4

![](img/9e15d853955818e4c3b0ae55b096.png)

Once again, monospaced output was used so that you can see multiple blanks. The variable Join is created by concatenation of the separator to the front and back of the variable. Notice that there are three blanks between Ron and Cody. The CAT function gives you the same result as the || operator. The CATS function strips leading and trailing blanks before joining the strings. Finally, Name4 has a single blank between the first and last names because a blank was entered as the separator value.

## 12.6 Removing Leading or Trailing Blanks

Three functions, TRIMN (remember the N is for null), LEFT, and STRIP enable you to remove trailing blanks, leading blanks, or both from a character value. We will demonstrate these functions with a sample program:

### Program 12.5: Demonstrating TRIMN, LEFT, and STRIP Functions

```sas
data Blanks;
  String = ' ABC ';
  JoinLeft = ':' || left(String);
  JoinTrim = ':' || trimn(String);
  JoinStrip = ':' || strip(String);
run;
```

Here is the output:

### Listing 12.5: Output from Data Set Blanks

| String | JoinLeft | JoinTrim | JoinStrip |
|---|---|---|---|
| ABC | :ABC | :ABC | :ABC |

The variable String has three leading and two trailing blanks. A good way to know if a value has leading or trailing blanks is to concatenate a character (a colon for example) to the beginning and end of character value. Note: It is very hard to see trailing blanks on output—only experienced SAS programmers can do this! The three Join variables, we have JoinLeft followed by five blanks, JoinTrim followed by three, and JoinStrip no trailing blanks. When you assign the result of any of these functions to a variable, the length of that variable does not change. So, if you create three variables in the following examples, the storage length of each of the three variables Left, Trim, Strip is equal to 8 (the length of String):

```sas
Left = left(String);
Trim = trimn(String);
Strip = strip(String);
```

## 12.7 Using the COMPRESS Function to Remove Characters from a String

Here's an interesting, and fairly common problem: you have a SAS data set (or raw data file) containing phone numbers. These numbers came from various sources and are in various formats, as shown here:

### Figure 12.6: Listing of Data Set Learn

| Phone |
|---|
| (908)232-4856 |
| 210.343-4757 |
| (516) 343-9293 |
| 93423425 |

You want to retain only the digits in each of these phone numbers and hyphens from each of the values. To do this, you want to remove blanks, left and close parentheses, periods, and hyphens. The COMPRESS function allows you to select which characters you want to remove from a character value. Here is one way to accomplish this task:

### Program 12.6: Using the COMPRESS Function to Remove Characters from a String

```sas
data Phone;
  length PhoneNumber $10;
  set Learn.Phone;
  PhoneNumber = compress(Phone, ' -.');
```

The first argument of the COMPRESS function is the character value from which you want to remove the characters. If you omit the second argument, COMPRESS removes all blanks from the string. A listing of data set Phone is shown next:

### Figure 12.7: Listing of Data Set Phone

| PhoneNumber | Phone |
|---|---|
| 9082324856 | (908)232-4856 |
| 2103434757 | 210.343-4757 |
| 5163439293 | (516) 343-9293 |
| 93423425 | 93423425 |

Notice that the character variable PhoneNumber contains only digits.
