

An assembly reference list is, in essence, a list of all external dependencies, such as .dlls or other files. Assembly references include references to both global and private objects. Global objects are accessible to all other applications. In .NET Core, global objects are coupled with a particular .NET Core runtime. In .NET Framework, global objects are housed in the GAC. System.IO.dll is a perfect example of an assembly in the GAC. Private objects must be in a directory level at or below the directory in which your app is installed.

## What Are the Benefits of Using Assemblies?

Assemblies are mainly introduced to sort out the problems of versioning, DLL conflicts, and simplifying deployment. Most end users have experienced versioning or deployment issues when installing a new version or a new application of an existing one. There are many circumstances where you install a new application only to find an existing one stopped working, and the system cannot recover from that. Many developers spent much of their time maintaining the registry entries consistency to activate a COM class. All this frustration happens because of versioning issues that occur with component-based applications.

### Versioning Problems

Two versioning problems occur with WIN32 applications. The versioning rules are enforced by the OS and are not between the pieces of an application. Backward compatibility between the new part of code and the old one is the current way of versioning, and this is almost impossible to maintain in most applications. Besides that, only a single version of an application is admitted and executed on a computer at any given point in time. The second issue is that there is no way to maintain consistency between components created together and the current present group at run time.

### DLL Conflicts

As a result of the above two versioning problems, DLL conflicts do emerge. When installing a new application, an existing one may break because the new one installed a new version of a component or a DLL that is not fully backward compatible enough with the previous one.

### The Solution

To sort out the above problems, Microsoft introduced a sophisticated way in its Windows 2000 platform. Windows 2000 provides you the capacity to place DLL files used by your application in the same directory as your application’s exe file to ensure use of the correct version designed for use. Besides that, Windows 2000 locks files that exist in the System32 directory to prevent their replacement when newer applications are installed, and this prevents the DLLs used by existing applications from being replaced and so averts the crashing of existing applications.

The .NET framework established assemblies as an evolution toward the complete solution of versioning problems and DLL conflicts. Assemblies, by their core design, allow developers to specify version rules between components, offer the infrastructure required to impose these rules, and enable different versions of the part to be run side by side simultaneously.

Taylor & Francis  
Taylor & Francis Group  
http://taylorandfrancis.com

## Data Types and Operators

### IN THIS CHAPTER

- Basic Data Types
- Variables
- Constants
- Reference Types and Value Types
- Arrays and Operators

In the previous chapter, we have covered the building blocks of C#, the .NET Frameworks, and Assemblies in .NET, and now we will discuss Data Types and Variables. A desktop application, scripted in any programming language, comprises three elements: data, operations on data, and the logic that determines the operations. Therefore, manipulating the data (i.e., holding and operating on it) is at the core of a typical computer program. Variables store the data, and the operations are made by using operators. A data type is a classification of data that tells the compiler or interpreter how the programmer intends to use the data. A data type stands for the type of data that a variable is able to store, such as integer, floating, character, etc.

There are three kinds of Data Types in C#.

| Types | Data Type |
| --- | --- |
| Value Data Type | Short, int, char, float, double, etc. |
| Reference Data Type | String, class, objects, and interface |
| Pointer Data Type | Pointers |

### VALUE DATA TYPE

The value data types are integer-based and floating-point based. C# language supports both signed and unsigned literals.

There are two types of value data types in C# language:

- **Predefined Data Types:** includes values like Integer, Boolean, Float
- **User-defined Data Types:** consists of Structure and Enumerations

The memory size of data types may vary from 32-bit or 64-bit operating systems.

Let’s take a look at the value data types size, given according to 32 bit OS:¹

| Data Type | Size | Range |
| --- | --- | --- |
| char | 1 byte | -128 to 127 |
| Signed char | 1 byte | -128 to 127 |
| Unsigned char | 1 byte | 0 to 255 |
| Short | 2 byte | -32,768 to 32,767 |
| Signed short | 2 byte | -32,768 to 32,767 |
| Unsigned short | 2 byte | 0 to 65,535 |
| Int | 4 byte | -2,147,483,648 to 2,147,483,647 |
| Signed int | 4 byte | -2,147,483,648 to 2,147,483,647 |
| Unsigned int | 4 byte | 0 to 4,294,967,295 |
| Long | 8 byte | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| Signed long | 8 byte | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| Unsigned long | 8 byte | 0 to 18,446,744,073,709,551,615 |
| Float | 4 byte | 1.5 * 10^-45 to 3.4 * 10^38, 7-digit precision |
| Double | 8 byte | 5.0 * 10^-324 to 1.7 * 10^308, 15-digit precision |
| Decimal | 16 byte | at least -7.9 * 10^28 to 7.9 * 10^28, with at least 28-digit precision |

### REFERENCE DATA TYPE

These particular data types do not include the real data stored in a variable, but they have a certain reference to the variables. Thus, in case the data is edited by one of the variables, the next variable will immediately reflect this modification in value.

There are two kinds of reference data types in the C# language.

- **Predefined Types:** such as objects, string.
- **User-defined Types:** such as classes, interface.

### Pointer Data Type

The pointer in the C# language is a variable, and it is also known as a locator or indicator that indicates an address of a value.

### Operators

Operators are the basic foundation of any programming language.² Thus the functionality of the C# language is insufficient without the use of operators. Operators let us perform different types of operations on operands. In C#, operators can be categorized according to their different functionality:

- Arithmetic operators.
- Relational operators.
- Logical operators.
- Bitwise operators.
- Assignment operators.
- Conditional operator.

In C#, operators can also be categorized based upon the number of operands:

- **Unary operator:** Operator that picks one operand to perform the operation.
- **Binary operator:** Operator that picks two operands to perform the operation.
- **Ternary operator:** Operator that picks three operands to perform the operation.

We will look into the details of different operators in the last part of this chapter.

### BASIC DATA TYPES IN C#

The C# language brings with it a set of basic data types. These data types are always used to build values that are applied within an application. Let’s dive into the basic data types out there in C#. For every example, we will modify just the main function in our Program.cs file.

#### Integer

An Integer data type is always used to operate with numbers. And when we say numbers, we specifically mean the whole numbers such as 20, 30, or 40. Additionally, in C# the datatype is marked by the Int32 keyword. Let us look at an example of how this data type can be used. In our example, we will declare an Int32 variable called num.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace DemoApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            Int32 num=30;
            Console.Write(num);
            Console.ReadKey();
        }
    }
}
```

- **Code explanation:** The above Int32 data type is set to include an Integer variable called num. The variable is then given a value of 30. As for the console, make sure you add the `Console.Write` function, which is used to output the number to the console.

#### Double

A double data type is great to operate with decimals. Similar to the above data type, the numbers should be the real numbers like 20.21, 30.32, or 40.43. This particular datatype is marked by the keyword “Double.” To illustrate with an example:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```
