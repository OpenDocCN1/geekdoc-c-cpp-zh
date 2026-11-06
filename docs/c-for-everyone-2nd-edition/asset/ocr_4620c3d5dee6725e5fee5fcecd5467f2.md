![](bbox=[0.0, 0.0, 0.384, 0.175])

Numbers and character strings (such as the ones on this display board) are important data types in any C++ program. In this chapter, you will learn how to work with numbers and text, and how to write simple programs that perform useful tasks with them.

# 2.1 Variables

When your program carries out computations, you will want to store values so that you can use them later. In a C++ program, you use variables to store values. In this section, you will learn how to define and use variables.

To illustrate the use of variables, we will develop a program that solves the following problem. Soft drinks are sold in cans and bottles. A store offers a six-pack of 12-ounce cans for the same price as a two-liter bottle. Which should you buy? (12 fluid ounces equal approximately 0.355 liters.)

In our program, we will define variables for the number of cans per pack and for the volume of each can. Then we will compute the volume of a six-pack in liters and print out the answer.

![](bbox=[0.585, 0.316, 0.896, 0.481])

What contains more soda? A six-pack of 12-ounce cans or a two-liter bottle?

# 2.1.1 Variable Definitions

The following statement defines a variable named `cans_per_pack`:

```
int cans_per_pack = 6;
```

A variable is a storage location with a name.

A variable is a storage location in a computer program. Each variable has a name and holds a value.

A variable is similar to a parking space in a parking garage. The parking space has an identifier (such as “J 053”), and it can hold a vehicle. A variable has a name (such as `cans_per_pack`), and it can hold a value (such as 6).

![](bbox=[0.477, 0.731, 0.865, 0.906])

Like a variable in a computer program, a parking space has an identifier and a contents.