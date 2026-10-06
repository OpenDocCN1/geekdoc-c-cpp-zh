11.7 A program that uses a multiple-level menu typically displays a main menu when the program starts, showing only a few items, and then displays smaller submenus when the user makes a selection.

11.8 Users often have trouble sorting through the items in the menu when given too many choices.

# Chapter 12

+   12.1 y

+   12.2 Set str[0] ="L"

```
12.3 if isDigit(str[0]) Then
    delete(str, 0, 0)
    End If
```

```
12.4 if isUpperCase(str[0]) Then
    Set str[0] = "0"
    End If
```

+   12.5 insert(str, 0,"Hello )

+   12.6 delete(city, 0, 2)

# Chapter 13

+   13.1 A recursive algorithm requires multiple method calls. Each method call requires several actions to be performed by the computer. These actions include allocating memory for parameters and local variables, and storing the address of the program location where control returns after the method terminates. All of these actions are known as overhead. In an iterative algorithm, which uses a loop, such overhead is unnecessary.

+   13.2 A case in which the problem can be solved without recursion.

+   13.3 A case in which the problem is solved using recursion.

+   13.4 When it reaches the base case.

+   13.5 In direct recursion, a recursive method calls itself. In indirect recursion, method A calls method B, which in turn calls method A.

# Chapter 14

+   14.1 An object is a software entity that contains both data and procedures.

+   14.2 Encapsulation is the combining of data and code into a single object.

+   14.3 When an object's internal data is hidden from outside code and access to that data is restricted to the object's methods, data is protected from accidental recursion. In addition, the programming code outside the object does not need to know about the format or internal structure of the object's data.

+   14.4 Public methods can be accessed by entities outside the object. Private methods cannot be accessed by entities outside the object. They are designed to be accessed internally.