```
```text
'h', 'i', 'j', 'k', 'l', 'm'};

// all in one
int[] array4 = new int[] { 1, 2, 3};
// split
int[] array4;
array4 = new int[] { 1, 2, 3};
// shorthand
int[] array4 = {1, 2, 3};
```
```

> > Here, the brackets are used to indicate that a value is an array. The assignment statement is always enclosed by two braces and again, commas are required to separate those values. Single quotation marks are also used to store single character values and the assignments themselves can be used to replace the formal parameters.

![](bbox=[0.802, 0.294, 0.922, 0.378])

Another useful tool is to include a *string value reference*, replacing the older value type character array with a dynamic value. This new format eliminates the need to make arbitrary guestimations about string size, and thus will be much less likely that we'll have to tamper with the coding in order to deal with any unusual changes (see Example 4.8).

# Example 4.8. String value reference.

```
```text
string String1 = "Damn it boy, its three o'clock in the morning."
string String2 = "What the hell are you doing up so late? \n";
string String3 = "I'm just doing my homework Dad.\n";
string String4 = "Oh, I know what you're doing, turn those games off and
                  go to bed! \n";
string String5 = "That's it! I'm quitting school and joining a software
                  company! \n";
string String6 = "Oh no you're not mister! We didn't raise you to develop
                  software! \n";
```
```