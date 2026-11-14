a very solid IDE allowing for productive development under Windows and in newer versions also supports an integration of CMake projects.

To find the most productive environment takes some time and experimentation and is of course subject to personal and collaborative taste. As such, it will also evolve over time.

# 1.2 Variables

C++ is a strongly typed language (in contrast to many scripting languages). This means that every variable has a type and this type never changes. A variable is declared by a statement beginning with a type followed by a variable name with optional initialization—or a list thereof:

Click here to view code image

```
int i1 = 2; // Alignment for readability only
int i2, i3= 5; // Note: i2 is not initialized
float pi= 3.14159;
double x= -1.5e6; // -1500000
double y= -1.5e-6; // -0.0000015
char c1= 'a', c2= 35;
cmp= i1 < pi, // -> true
happy= true;
```

The two slashes // here start a single-line comment; i.e., everything from the double slashes to the end of the line is ignored. In principle, this is all that really matters about comments. So as not to leave you with the feeling that something important on the topic is still missing, we will discuss it a little more in Section 1.9.1.

# 1.2.1 Intrinsic Types

The most fundamental types in C++ are the Intrinsic Types listed in Table 1–1. They are part of the core language and always available.

# Table 1–1: Intrinsic Types

| Name | Semantics |
| :--- | :--- |
| char | letter and very short integer number |