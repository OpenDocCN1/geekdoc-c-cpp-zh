# Writing Methods with No Parameters and No Return Value

| Access modifier (If omitted, it private) | Optional static modifier | Method return type | Method name |
| --- | --- | --- | --- |
| Method header (usually written on a single line) | | | |
| Method body between curly braces | | | |

Optionally, method parameters could appear between these parentheses

**Figure 7-2** The WelcomeMessage() method

# # Introduction to Accessibility

The declared **accessibility** for a method sets limits as how other methods can use your method; accessibility can be any of the levels described in Table 7-1. The two levels you will use most frequently, **public** and **private** access, are shaded in the table. You will learn about protected access and what it means to derive types in the chapter "Inheritance."

+   * **Public access** is established by including a public modifier in the member declaration. This modifier allows access to the method from other classes.
* **Private access** is established by including a private modifier in the member declaration or by omitting any accessibility modifier. This limits method access to the class that contains the method.

| Decl accessibility | Can methods contained in the same class access this method? | Can derived classes access this method? | Can assemblies or projects contain this class access this method? | Can any class access this methods? |
| --- | --- | --- | --- | --- |
| **public** | Yes | Yes | Yes | Yes |
| **protected internal** | Yes | Yes | No | No |
| **protected** | Yes | No | Yes | No |
| **internal** | Yes | No | Yes | No |
| **private** | Yes | No | No | No |

**Table 7-1** Summary of method accessibility

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 022-200-222