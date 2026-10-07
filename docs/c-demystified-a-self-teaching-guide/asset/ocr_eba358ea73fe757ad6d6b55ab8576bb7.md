# Using the switch Statement with Logical Operators

The switch statement was discussed at some length in Chapter 5. However, so far in this chapter it has been conspicuous by its absence.

In Chapter 5, we discussed how the switch statement was cumbersome when dealing with a range of numbers. The reason was that the case could not be followed by a range of numbers it must instead be followed by a single integer.

However, the switch statement may be used with expressions that use the Logical And Or operator. The reason is that these expressions have only one of two values, true or false. True and false are both constants; the value of true is true and the value of false is false. While true and false are Boolean values, each has a corresponding integer value:1 and 0. Therefore, the case may be followed by true or false, just as in Chapter where the case could be followed by a character since that has a corresponding integer ANSI or ASCII value.

For example, earlier in this chapter the Logical And operator was used in the following determining whether the user is eligible to vote, the criteria that the user must be at least 18 years and old.

```
if (age >= 18 && citizen == true)
    cout << "You are eligible to vote";
else
    cout << "You are not eligible to vote";
```

The corresponding switch statement is

```
switch (age >= 18 && citizen == true)
{
    case true:
        cout << "You are eligible to vote";
        break;
    case false:
        cout << "You are not eligible to vote";
}
```

Also in this chapter, the Logical Or operator was used in the if/else structure determining whether the user gets into a movie free, the criteria that the user must be under 18 or over 65 years old.

```
if (age <= 12 || age >= 65)
    cout << "Admission is free";
else
    cout << "You have to pay";
```

The corresponding switch statement is

```
switch (age <= 12 || age >= 65)
{
    case true:
        cout << "Admission is free";
        break;
    case false:
        cout << "You have to pay";
}
```