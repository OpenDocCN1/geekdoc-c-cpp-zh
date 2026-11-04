
we use the cast operator to convert the int value in sumOfDice to type DiceNames and compare it to each of the constants in DiceNames. Lines 35–36 determine whether the player won on the first roll with Seven (7) or YoLeven (11). Lines 39–41 determine whether the player lost on the first roll with SnakeEyes (2), Trey (3) or BoxCars (12). After the first roll, if the game is not over, the default case (lines 44–48) saves sumOfDice in myPoint (line 46) and displays the point (line 47).

### Additional Rolls of the Dice
If we're still trying to "make our point" (i.e., the game is continuing from a prior roll), the loop in lines 52–69 executes. Line 54 rolls the dice again. If sumOfDice matches myPoint in line 57, line 59 sets gameStatus to Status.Won, and the loop terminates because the game is complete. In line 64, we use the cast operator (int) to obtain the underlying value of DiceNames.Seven so that we can compare it to sumOfDice. If sumOfDice is equal to Seven (7), line 66 sets gameStatus to Status.Lost, and the loop terminates because the game is over. When the game completes, lines 72–79 display a message indicating whether the player won or lost, and the app terminates.

### Control Statements in the Craps Example
Note the use of the various program-control mechanisms we've discussed. The Craps class uses two methods—Main and RollDice (called twice from Main)—and the switch, while, if...else and nested if control statements. Also, notice that we use multiple case labels in the switch statement to execute the same statements for sums of Seven and YoLeven (lines 35–36) and for sums of SnakeEyes, Trey and BoxCars (lines 39–41).

### Code Snippets for Auto-Implemented Properties
Visual Studio has a feature called code snippets that allows you to insert predefined code templates into your source code. One such snippet enables you to easily create a switch statement with cases for all possible values for an enum type. Type switch in the C# code then press Tab twice. If you specify a variable of an enum type in the switch statement's expression and press Enter, a case for each enum constant will be generated automatically.

To get a list of all available code snippets, type Ctrl + k, Ctrl + x. This displays the Insert Snippet window in the code editor. You can navigate through the Visual C# snippet folders with the mouse to see the snippets. This feature also can be accessed by right clicking in the source code editor and selecting the Insert Snippet... menu item.

## 7.10 Scope of Declarations
You've seen declarations of C# entities, such as classes, methods, properties, variables and parameters. Declarations introduce names that can be used to refer to such C# entities. The scope of a declaration is the portion of the app that can refer to the declared entity by its unqualified name. Such an entity is said to be "in scope" for that portion of the app. This section introduces several important scope issues. The basic scope rules are as follows:

- 1. The scope of a parameter declaration is the body of the method in which the declaration appears.
- 2. The scope of a local-variable declaration is from the point at which the declaration appears to the end of the block containing the declaration.
- 3. The scope of a local-variable declaration that appears in the initialization section of a for statement's header is the body of the for statement and the other expressions in the header.
- 4. The scope of a method, property or field of a class is the entire body of the class. This enables non-static methods and properties of a class to use any of the class's fields, methods and properties, regardless of the order in which they're declared. Similarly, static methods and properties can use any of the static members of the class.

Any block may contain variable declarations. If a local variable or parameter in a method has the same name as a field, the field is hidden until the block terminates—in Chapter 10, we discuss how to access hidden fields. A compilation error occurs if a nested block in a method contains a variable with the same name as a local variable in an outer block of the method. The app in Fig. 7.8 demonstrates scoping issues with fields and local variables.

### Error-Prevention Tip 7.1
Use different names for fields and local variables to help prevent subtle logic errors that occur when a method is called and a local variable of the method hides a field of the same name in the class.

```
// Fig. 7.8: Scope.cs
// Scope class demonstrates static- and local-variable scopes.
using System;

class Scope
{
    // static variable that's accessible to all methods of this class
    private static int x = 1;

    // Main creates and initializes local variable x
    // and calls methods UseLocalVariable and UseStaticVariable
    static void Main()
    {
        int x = 5; // method's local variable x hides static variable x

        Console.WriteLine("local x in method Main is {x}");

        // UseLocalVariable has its own local x
        UseLocalVariable();

        // UseStaticVariable uses class Scope's static variable x
        UseStaticVariable();

        // UseLocalVariable reinitializes its own local x
        UseLocalVariable();

        // class Scope's static variable x retains its value
        UseStaticVariable();
    }
}
```

Fig. 7.8 | Scope class demonstrates static- and local-variable scopes. (Part 1 of 2.)

```csharp
29     Console.WriteLine($"\nlocal x in method Main is {x}");
30 }
31
32     // create and initialize local variable x during each call
33     static void UseLocalVariable()
34     {
35         int x = 25; // initialized each time UseLocalVariable is called
36
37         Console.WriteLine(
38             $"\nlocal x on entering method UseLocalVariable is {x}");
39         ++x; // modifies this method's local variable x
40         Console.WriteLine(
41             $"local x before exiting method UseLocalVariable is {x}");
42     }
43
44     // modify class Scope's static variable x during each call
45     static void UseStaticVariable()
46     {
47         Console.WriteLine("static variable x on entering method " +
48             $"UseStaticVariable is {x}");
49         x *= 10; // modifies class Scope's static variable x
50         Console.WriteLine("static variable x before exiting " +
51             $"method UseStaticVariable is {x}");
52     }
53 }
54
```

```text
local x in method Main is 5

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 1
static variable x before exiting method UseStaticVariable is 10

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 10
static variable x before exiting method UseStaticVariable is 100

local x in method Main is 5
```

Fig. 7.8 | Scope class demonstrates static- and local-variable scopes. (Part 2 of 2.)

Line 8 declares and initializes the static variable x to 1. This static variable is hidden in any block (or method) that declares a local variable named x. Method Main (lines 12–31) declares local variable x (line 14) and initializes it to 5. This local variable's value is output to show that static variable x (whose value is 1) is hidden in method Main. The app declares two other methods—UseLocalVariable (lines 34–43) and UseStaticVariable (lines 46–53)—that each take no arguments and do not return results. Method Main calls each method twice (lines 19–28). Method UseLocalVariable declares local variable x (line 36). When UseLocalVariable is first called (line 19), it creates local variable x and

another method, a stack frame for the new method call is simply *pushed* onto the call stack. Thus, the return address required by the newly called method to return to its caller is now located at the *top* of the stack.

## 7.11.3 Local Variables and Stack Frames
The stack frames have another important responsibility. Most methods have local variables—parameters and any local variables the method declares. Local variables need to exist while a method is executing. They need to remain active if the method makes calls to other methods. But when a called method returns to its caller, the called method's local variables need to "go away." The called method's stack frame is a perfect place to reserve the memory for the called method's local variables. That stack frame exists as long as the called method is active. When that method returns—and no longer needs its local variables—its stack frame is *popped* from the stack, and those local variables no longer exist.

## 7.11.4 Stack Overflow
Of course, the amount of memory in a computer is finite, so only a certain amount of memory can be used to store activation records on the method-call stack. If more method calls occur than can have their activation records stored on the method-call stack, a fatal error known as stack overflow occurs—typically caused by infinite recursion (Section 7.16).

## 7.11.5 Method-Call Stack in Action
Now let's consider how the call stack supports the operation of a Square method (lines 15–18 of Fig. 7.9) called by Main (lines 8–12).

```csharp
// Fig. 7.9: SquareTest.cs
// Square method used to demonstrate the method
// call stack and activation records.
using System;

class Program
{
    static void Main()
    {
        int x = 10; // value to square (local variable in main)
        Console.WriteLine($"x squared: {Square(x)}");
    }

    // returns the square of an integer
    static int Square(int y) // y is a local variable
    {
        return y * y; // calculate square of y and return result
    }
}
```

**Fig. 7.9** | Square method used to demonstrate the method-call stack and activation records. (Part 1 of 2)

2. This is how the website stackoverflow.com got its name. This is a popular website for getting answers to your programming questions.
