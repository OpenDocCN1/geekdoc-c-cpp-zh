(the maximum value that an sbyte can hold is 127) the compiler will detect that I have made a mistake and the program will not compile.

# Storing real values

"Real" is a generic term for numbers which are not integers. They have a decimal point and a fractional part. Depending on the value the decimal point floats around in the number, hence the name float.

C# provides a type of box which can hold a real number. A standard float value has a range of 1.5E-45 to 3.4E48 with a precision of only 7 digits (i.e. not as good as most pocket calculators).

If you want more precision (although of course your programs will use up more computer memory and run more slowly) you can use a double box instead (double is an abbreviation for double precision). This takes up more computer memory but it has a range of 5.0E-324 to 1.7E308 and a precision of 15 digits.

An example of a float variable could be something which held the average price of ice cream:

```
float averageIceCreamPriceInPence;
```

An example of a double variable could be something which held the width of the universe in inches;

```
double uniWidthInInches;
```

Finally, if you want the ultimate in precision but require a slightly smaller range you can use the decimal type. This uses twice the storage space of a double and holds values to a precision of 28-29 digits. It is used in financial calculations where the numbers are not so large but they need to be held to very high accuracy.

```
decimal robsOverdraft;
```

# real literal values

There are two ways in which you can store floating point numbers: as float or as double. When it comes to putting literal values into the program itself the compiler likes to know if you are writing a floating point value (smaller sized box) or double precision (larger sized box).

A float literal can be expressed as a real number with an f after it:

```
2.5f
```

A double literal is expressed as a real number without the f:

```
3.5
```

You can also use exponents to express double and float values:

```
9.4665288415
```

This is a double precision literal value which is actually the number of meters in a light year. If you put an f on the end it becomes a floating point literal value.

Unlike the way that integers work, with real numbers the compiler is quite fussy about how they can and can't be combined. This is because when you move a value from a double precision variable into an ordinary floating point one some of the precision is lost. This means that you have to take special steps to make sure that you as programmer make clear that you want this to happen and that you can live with the consequences. This process is known as casting and we will consider it in detail a bit later.