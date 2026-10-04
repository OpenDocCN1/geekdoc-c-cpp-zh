# Chapter 2

Variables and Declaration Statements

In C++, the selection of variable names is the programmer's choice, as are the rules listed in Section 2.1 for selecting identifier names are observed. These rules are summarized in the following list:

+   1. The variable name must begin with a letter or underscore (_) and can contain only letters, underscores, or digits. It cannot contain blank spaces, commas, or special symbols, such as (&), #.
2. A variable name cannot be a keyword (see Table 2.1).
3. A variable name cannot consist of more than 1024 characters.

Additionally, variable names should be mnemonics that give some indication of the variable's purpose. For a variable used to store a value that's the total of all values, a good name is sum or total. Variable names giving no indication of the value stored, such as r2d2, linda, and getum, shouldn't be used. With function names, variable names can consist of uppercase and lowercase letters.

Assume the first memory location shown in Figure 2.9, which has the address 1652, and the name num1. The memory location 2548 is given the variable name num2, and memory location 3000 is given the variable name total.

# Variable names

![](bbox=[0.237, 0.447, 0.762, 0.578])

**Figure 2.9** Naming storage locations

Using these variables, the operation of storing 45 in location 1652, and adding the contents of these two locations is accomplished by these C++ statements:

```
num1 = 45;
num2 = 12;
total = num1 + num2;
```

Each of these statements is called an **assignment statement** because it tells the computer to assign (store) a value in a variable. Assignment statements always have an equal sign (=) and one variable name immediately to the left of the =. The value to the right of the equal sign is determined first; value this is then assigned to the variable for readability. Assignment statements are explained in more detail in Chapter 3, but for now, just know that you can use them to store values in variables.

A variable is useful because it frees programmers from having to think about where data is physically stored in the computer. You simply use the variable and let the compiler worry about where in memory the data is actually stored. Before storing a value in