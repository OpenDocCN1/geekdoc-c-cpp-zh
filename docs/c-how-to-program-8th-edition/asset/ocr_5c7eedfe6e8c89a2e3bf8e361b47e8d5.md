```
```cpp
int number1; // first integer to add
```
```

could have been placed immediately before line 14

```
```cpp
std::cin >> number1; // read first integer from user into number1
```
```

the declaration in line 10

```
```cpp
int number2; // second integer to add
```
```

could have been placed immediately before line 17

```
```cpp
std::cin >> number2; // read second integer from user into number2
```
```

and the declaration in line 11

```
```cpp
int sum; // sum of number1 and number2
```
```

could have been placed immediately before line 19

```
```cpp
sum = number1 + number2; // add the numbers; store result in sum
```
```

> > **Good Programming Practice 2.8**
> >
> > *Always place a blank line between a declaration and adjacent executable statements. This makes the declarations stand out and contributes to program clarity.*

![](bbox=[0.159, 0.398, 0.219, 0.438])

# Obtaining the First Value from the User

Line 13

```
```cpp
std::cout << "Enter first integer: "; // prompt user for data
```
```

displays Enter first integer: followed by a space. This message is called a prompt because it directs the user to take a specific action. We like to pronounce the preceding statement as “std::cout gets the character string "Enter first integer: "." Line 14

```
```cpp
std::cin >> number1; // read first integer from user into number1
```
```

uses the standard input stream object cin (of namespace std) and the stream extraction operator, >>, to obtain a value from the keyboard. Using the stream extraction operator with std::cin takes character input from the standard input stream, which is usually the keyboard. We like to pronounce the preceding statement as, “std::cin gives a value to number1” or simply “std::cin gives number1.”

When the computer executes the preceding statement, it waits for the user to enter a value for variable number1. The user responds by typing an integer (as characters), then pressing the Enter key (sometimes called the Return key) to send the characters to the computer. The computer converts the character representation of the number to an integer and assigns (i.e., copies) this number (or value) to the variable number1. Any subsequent references to number1 in this program will use this same value.

The std::cout and std::cin stream objects facilitate interaction between the user and the computer. Because this interaction resembles a dialog, it’s often called interactive computing.

# Obtaining the Second Value from the User

Line 16

```
```cpp
std::cout << "Enter second integer: "; // prompt user for data
```
```