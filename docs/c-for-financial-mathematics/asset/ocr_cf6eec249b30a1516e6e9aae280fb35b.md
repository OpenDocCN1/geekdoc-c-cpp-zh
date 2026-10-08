+   - A single binary digit is called a bit. This is just a truncation of the phrase binary digit.

- 8 binary digits are called a byte. This is just a bad joke.

- 1024 bytes make a kilobyte (1024 = $2^{10}$ so the usual use of “kilo” to mean 1000 is tweaked to work better in binary).

- 1048576 = $2^{20}$ bytes make up a megabyte.

- Numbers representing memory locations are often written in hexadecimal. This is base 16. The 16 characters 0, 1, 2, \dots, 9, A, B, C, D, E, and F are used to represent hexadecimal digits. So A is equivalent to the decimal number 10 and F to the decimal number 15. The hexadecimal number 10 can be written in decimal as 16. Four binary digits are equivalent to one hexadecimal digit. For this reason, one hexadecimal digit is called a nibble.

As is already clear, computer programmers have a particularly poor sense of humour.

> **Old Joke:** There are 10 kinds of people. Those who understand binary, and those who don’t.

# 2.2 Basic data types

# 2.2.1 Integers

You can assign a fixed value to a variable of type int using the = operator as follows.

```
```cpp
int numberOfPlatonicSolids = 5;
```
```

When you type an integer you should not include any commas or spaces. So don’t write 1,000,000, simply write 1000000.
If you like you can specify an integer using a different numeric base. For example, if you prefer counting in hexadecimal (base 16) you can type 0xFF instead of 255. The prefix 0x means “This number is in hexadecimal”.
Confusingly, the prefix 0 on its own means “This number is in base 8” So the code

```
```cpp
int numberOfPlanets = 08;
```
```