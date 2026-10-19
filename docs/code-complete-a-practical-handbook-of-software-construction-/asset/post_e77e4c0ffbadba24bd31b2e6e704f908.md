
## Visual Basic Example of Copying a Group of Data Items Clumsily

```
newName = oldName
newAddress = oldAddress
newPhone = oldPhone
newSsn = oldSsn
newGender = oldGender
newSalary = oldSalary
```

Every time you want to transfer information about an employee, you have to have this whole group of statements. If you ever add a new piece of employee information—for example, numWithholdings—you have to find every place at which you have a block of assignments and add an assignment for newNumWithholdings = oldNumWithholdings.

Imagine how horrible swapping data between two employees would be. You don’t have to use your imagination—here it is:

![](img/649c8eee28c38ca1e062691e45dc9883_357_0.png)

## Visual Basic Example of Swapping Two Groups of Data the Hard Way

```
* swap new and old employee data
previousOldName = oldName
previousOldAddress = oldAddress
previousOldPhone = oldPhone
previousOldSsn = oldSsn
previousOldGender = oldGender
previousOldSalary = oldSalary

oldName = newName
oldAddress = newAddress
oldPhone = newPhone
oldSsn = newSsn
oldGender = newGender
oldSalary = newSalary

newName = previousOldName
newAddress = previousOldAddress
newPhone = previousOldPhone
newSsn = previousOldSsn
newGender = previousOldGender
newSalary = previousOldSalary
```

An easier way to approach the problem is to declare a structured variable:

## Visual Basic Example of Declaring Structures

```
Structure Employee
    name As String
    address As String
    phone As String
    ssn As String
    gender As String
    salary As Long
```

```
End Structure
Dim newEmployee As Employee
Dim oldEmployee As Employee
Dim previousOldEmployee As Employee
```

Now you can switch all the elements in the old and new employee structures with three statements:

```
Visual Basic Example of an Easier Way to Swap Two Groups of Data
previousOldEmployee = oldEmployee
oldEmployee = newEmployee
newEmployee = previousOldEmployee
```

If you want to add a field such as numWithholdings, you simply add it to the Structure declaration. Neither the three statements above nor any similar statements throughout the program need to be modified. C++ and other languages have similar capabilities.

> Cross-Reference For details on how much data to share between routines, see "Keep Coupling Loose" in Section 5.3.

## Use structures to simplify parameter lists

You can simplify routine parameter lists by using structured variables. The technique is similar to the one just shown. Rather than passing each of the elements needed individually, you can group related elements into a structure and pass the whole enchilada as a group structure. Here’s an example of the hard way to pass a group of related parameters:

```
Visual Basic Example of a Clumsy Routine Call Without a Structure
HardWayRoutine( name, address, phone, ssn, gender, salary )
```

And this is an example of the easy way to call a routine by using a structured variable that contains the elements of the first parameter list:

```
Visual Basic Example of an Elegant Routine Call with a Structure
EasyWayRoutine( employee )
```

If you want to add numWithholdings to the first kind of call, you have to wade through your code and change every call to HardWayRoutine(). If you add a numWithholdings element to Employee, you don’t have to change the parameters to EasyWayRoutine() at all.

> Cross-Reference For details on the hazards of passing too much data, see "Keep Coupling Loose" in Section 5.3.

You can carry this technique to extremes, putting all the variables in your program into one big, juicy variable and then passing it everywhere. Careful programmers avoid bundling data any more than is logically necessary. Furthermore, careful programmers avoid passing a structure as a parameter when only one or two fields from the structure are needed—they pass the specific fields needed instead. This is an aspect of information hiding: some information is hidden in routines, and some is hidden from routines. Information is passed around on a need-to-know basis.

## Use structures to reduce maintenance

Because you group related data when you use structures, changing a structure requires fewer changes throughout a program. This is especially true in sections of code that aren’t logically related to the change in the structure. Since changes tend to produce errors, fewer changes mean fewer errors. If your *Employee* structure has a *title* field and you decide to delete it, you don’t need to change any of the parameter lists or assignment statements that use the whole structure. Of course, you have to change any code that deals specifically with employee titles, but that is conceptually related to deleting the *title* field and is hard to overlook.

The big advantage of structured the data is found in sections of code that bear no logical relation to the *title* field. Sometimes programs have statements that refer conceptually to a collection of data rather than to individual components. In such cases, individual components, such as the *title* field, are referenced merely because they are part of the collection. Such sections of code don’t have any logical reason to work with the *title* field specifically, and those sections are easy to overlook when you change *title*. If you use a structure, it’s all right to overlook such sections because the code refers to the collection of related data rather than to each component individually.

## 13.2 Pointers

![](img/649c8eee28c38ca1e062691e45dc9883_359_0.png)

Pointer usage is one of the most error-prone areas of modern programming, to such an extent that modern languages like Java, C#, and Visual Basic don’t provide a pointer data type. Using pointers is inherently complicated, and using them correctly requires that you have an excellent understanding of your compiler’s memory-management scheme. Many common security problems, especially buffer overruns, can be traced back to erroneous use of pointers (Howard and LeBlanc 2003).

Even if your language doesn’t require you to use pointers, a good understanding of pointers will help your understanding of how your programming language works. A liberal dose of defensive programming practices will help even further.

## Paradigm for Understanding Pointers

Conceptually, every pointer consists of two parts: a location in memory and a knowledge of how to interpret the contents of that location.

## Location in Memory

The location in memory is an address, often expressed in hexadecimal notation. An address on a 32-bit processor would be a 32-bit value, such as 0x0001EA40. The pointer itself contains only this address. To use the data the pointer points to, you have to go to that address and interpret the contents of memory at that location. If you were to look at the memory in that location, it would be just a collection of bits. It has to be interpreted to be meaningful.

## Knowledge of How to Interpret the Contents

The knowledge of how to interpret the contents of a location in memory is provided by the base type of the pointer. If a pointer points to an integer, what that really means is that the compiler interprets the memory location given by the pointer as an integer. Of course, you can have an integer pointer, a string pointer, and a floating-point pointer all pointing at the same memory location. But only one of the pointers interprets the contents at that location correctly.

In thinking about pointers, it’s helpful to remember that memory doesn’t have any inherent interpretation associated with it. It is only through use of a specific type of pointer that the bits in a particular location are interpreted as meaningful data.

Figure 13-1 shows several views of the same location in memory, interpreted in several different ways.

![](img/649c8eee28c38ca1e062691e45dc9883_360_0.png)

**Figure 13-1**  The amount of memory used by each data type is shown by double lines.

In each of the cases in Figure 13-1, the pointer points to the location containing the hex value 0x0A. The number of bytes used beyond the 0A depends on how the memory is interpreted. The way memory contents are used also depends on how the memory is
