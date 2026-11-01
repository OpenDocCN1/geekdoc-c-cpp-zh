Table 1.1 Commonly Used Types

| Type | Values |
|------|--------|
| short int | -32,768 to 32,767 |
| unsigned short int | 0 to 65,535 |
| int | -2,147,483,648 to 2,147,483,647 |
| unsigned int | 0 to 4,294,967,295 |
| long int | -2,147,483,648 to 2,147,483,647 |
| unsigned long int | 0 to 4,294,967,295 |
| float | 3.4E +/- 38 (seven significant digits) |
| double | 1.7E +/- 308 (15 significant digits) |
| long double | 1.7E +/- 308 (15 significant digits) |
| char | 256 character values |
| bool | true or false |

# Declaring Variables

All right, now that you've got a basic understanding of types, it's time to get back to the program. One of the first things I do is declare a variable (request that it be created) with the line:

```
int score;
```

In this code, I declare a variable of type `int`, which I name `score`. You use a variable name to access the variable. You can see that to declare a variable you specify its type followed by a name of your choosing. Because the declaration is a statement, it must end with a semicolon.

I declare three more variables of yet three more types in the next three lines. `distance` is a variable of type `double`. `playAgain` is a variable of type `char`. And `shieldsUp` is a variable of type `bool`.

Games (and all major applications) usually require lots of variables. Fortunately, C++ allows you to declare multiple variables of the same type in a single statement. That's just what I do next in the line.

```
short lives, aliensKilled;
```

This line establishes two short variables—`lives` and `aliensKilled`.