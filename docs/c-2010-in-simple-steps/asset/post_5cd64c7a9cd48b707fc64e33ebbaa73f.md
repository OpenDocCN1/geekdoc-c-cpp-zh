
## Note

Extending the functionalities and behavior of a class in another class is called Inheritance.

- **Delegate:** Refers to the objects that store references of the methods whose signatures match with the signature of the delegate. Delegates are the reference types that encapsulate a method with a specific signature.
- **Array:** Refers to an ordered arrangement of data elements. It is a data structure that contains a number of variables of the same data type at contiguous locations of the memory.

Now, let's learn about pointer types in C# 2010.

## Pointer Types

To maintain type safety and security in the context of references, C# uses delegates and does not support pointers. However, you can use the unsafe keyword to define an unsafe context where you can use pointers. In other words, pointer types are used only in the unsafe context. Pointer types are not inherited from the Object base class, which is the base class of all .NET types. You cannot convert pointer types to Object types and vice-versa. A pointer variable is used to store the address of another variable. The following syntax displays the declaration of pointer type:

```
datatype* identifier;
```

You have learned about data types in C#, further you learn about variables and constants.

## Working with Variables and Constants

A variable is an identifier that denotes a storage location in memory. Using the name of a variable in a program you can refer to the information stored at a particular location. Unlike, the constants that remain unchanged during the execution of a program, a value of a variable can be changed any time. Every variable has a type that determines the values to be stored in it.

You can give any name to a variable but it should be meaningful because it makes the code more readable.

Some examples of meaningful variable names are salary, height, name, age, and total_marks.

Following are certain rules for naming C# variables:

- The name of the variable may consist of letters, and the underscore character (_).
- The name of the variable must not begin with a digit.
- The variable names using the uppercase and lowercase characters are distinct; for example, salary and SALARY are two different variables.
- The variable name should not be a keyword.
- The variable name should not contain spaces.

Table 2.3 shows the examples of valid and invalid variable names:

Table 2.3: Some Examples of Valid and Invalid C# Variable Names

| Variable Name | Status |
|---|---|
| salary | Legal |
| Total_amount | Legal |
| yearly_cost | Legal |
| _2010_tax | Legal, but not advised |
| Total#amount | illegal; contains the illegal character # |
| double | illegal; double is a keyword |
| 9number | illegal; first character is a digit |

On the other hand, constants are those values which are fixed and do not change during the execution of a program. For instance, the value of Pi is fixed, so it can be declared as a constant. Moreover, any value that you do not want to change can be declared as a constant. Let's learn to declare a variable in C#.

## Declaring Variables

Any information in a program that can vary must be stored in a named memory location called variable. After specifying a meaningful name and appropriate data type to a variable, it is declared in the program so that the compiler can easily recognize the variable declared with a specific data type.

> **Note**
> 
> *A compiler is software that converts a source code written in a programming language into a machine language, which a computer can understand.*

A variable declaration performs the following tasks:

- Tells the compiler the name of the variable
- Tells about the type of data a variable holds
- Decides the scope of a variable

Moreover, a variable must be declared before it is used in a program. To declare a variable, you must specify a data type to it according to the value assigned, followed by the name of the variable. The following is the syntax for declaring a variable:

```
datatype variable1, variable2, variable3,... variableN;
```

If the variables to be declared are more than one and have same data types, then you can declare the variables in the same line separated by a comma, as shown in the preceding syntax. A code line in C# always ends with a semi colon. The following are some examples of legal variable declaration:

- float length;
- int age;
- char b1, b2;
- double pi;
- decimal money;

## Assigning Values to Variables

After the declaration of a variable, you need to initialize its value. Initialization of a value to a variable means assigning a value to a variable. While initializing a variable, ensure that a variable is assigned a value before being used in a program. It is not mandatory to initialize a variable at the time of declaration. The syntax for initialization is as follows:

```
variableName = value;
```

or

```
variable1 = variable2 = variable3 = value;
```

Following is the syntax to initialize a variable at the time of declaration:

```
datatype variableName = value;
```

or

```
datatype variable1 = value, variable2 = value;
```

The following are some valid examples of initializing a variable:

```
int age = 23;
bool status = false;
float height = 164.5f;
char sex = 'f';
int a = 4, b = 6;
```

```
decimal d = 2.34M;
```

Let's learn to declare constants.

## Declaring Constants

As discussed earlier, constants are fixed values that cannot be changed during the execution of a program.

Following is the syntax to declare a constant:

```
const datatype constantname = value;
```

You must declare and then initialize a constant, as shown in the following code snippet to avoid an error:

```
const float PI = 3.14;
const int count = 4;
```

The values assigned to constants cannot be changed during the execution of a program. A constant can also be initialized using an expression, as shown in the following code snippet:

```
const int length = 10;
const int breadth = length * 2;
```

Moreover, you cannot use a non-constant value in an expression, which is used by a constant, as shown in the following code snippet:

```
int length = 10;
const int breadth = length * 2;
// This is illegal statement because it is using a non-constant value
```

Let's learn to declare Nullable type variables.

## Declaring Nullable Type Variables

Nullable types are the instances of System.Nullable<T> struct. Nullable structs use predefined value types with a Boolean null indicator. The predefined value type is also called the underlying type. A Boolean variable of a nullable type can be assigned true, false, or null value. You can create nullable types using the ? type modifier.

The syntax to declare a nullable type is as follows:

```
System.Nullable<T> variable or T? variable
```

In the preceding syntax, T is the underlying value type of the nullable type. T can be of any value type, such as int, float, or struct. However, it cannot be a reference type. For instance, int? is the nullable type for the type, int. In this example, int is the underlying type and ? is the Boolean null indicator. Similarly, float? is the nullable type for the value type, float. You cannot create nullable type on reference types as they already support null values.

You have learned to declare and assign values to variables and constants, let's learn operators and operator precedence in the following section.

## Working with Operators and Operator Precedence

In C#, we can use the value stored inside the variables and constants in the form of an expression. An expression is nothing but a set of language elements, arranged together to perform a specific task or computation. To write expressions, C# 2010 provides a complete set of language elements, such as variables, constants, operators, properties, and literals. A typical example of an expression is shown in the following code snippet:

```
int total= 2 + 3;
```

In the preceding code snippet, expression comprises of an integer variable, total, an assignment operator =, integer values 2 and 3, and the addition operator, +. The evaluation of the expression yields the result, 5, which is then assigned to the integer variable total.

Operators are nothing but special symbols that are used to specify some computation or other operations, such as arithmetic and logical operations on the operands. Therefore, operators specify the operations to be performed in the expression. The operators in C# 2010 fall under several categories, such as primary, unary, multiplicative, additive, shift, relational and type testing, equality, logical AND, logical XOR, logical OR, conditional AND, conditional OR, null-coalescing, conditional, assignment operators, and lambda expression. Table 2.4 lists different categories and the operators that fall within those categories:
