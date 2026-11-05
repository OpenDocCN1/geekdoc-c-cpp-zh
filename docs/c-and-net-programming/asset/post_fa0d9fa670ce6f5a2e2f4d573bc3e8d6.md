
The following statement is used to define the syntax to declare a value parameter.

```
<return type> MethodName ( <data type> variable name )
{
}
```

## 2.2 Passing parameters by reference

This method copies the reference to the memory location of an argument into the formal parameter. This means that changes made to the parameter affect the argument.

A reference parameter is the reference to the memory location of a parameter. In reference parameter new storage location is not created. It stores the value in the same memory location as the variable passed is in the memory call.

The declaration of the reference parameter is done by using the ref keyword. The example for the reference parameters is as shown below,

```
void ShowReference( ref int Id, ref int age )
{
}
```

## 2.3 Passing parameters using output parameters

In this method more than one value can be returned to the calling method.

A return statement is used for returning a value from the method. A return statement can be used to return only a single value. The output parameter is used to overcome this problem.

Output parameters are like reference parameters but they transfer data out of the method. An output parameter is reference to the storage location supplied by the caller. To declare an output parameter, the out keyword is used before the data type and the variable name.

Out parameters are specified as shown below,

```
static void Outsample( out int i )
{
    i=20;
}
```

## 2.4 Variable number of arguments to the method

A method can take variable number of arguments. For this the params keyword is used. No additional parameters are permitted after the params keyword.

Only one params keyword is permitted in a method declaration.

### Example

```csharp
//illustration of variable number of arguments
/* GetSum() method is called twice. In first call , it takes 3 arguments, in the second call 5.
static void GetSum(params int[] list)
{
...
}
The GetSum() method can take variable number of integer values. All values are added to
    the list array.  */
using System;
public class SumValues
{
    static void Main()
    {
        GetSum(10, 20, 30);
        GetSum(10, 20, 30, 40, 50);
    }

    static void GetSum(params int[] numlist)
    {
        Console.WriteLine("There are {0} numbers", numlist.Length);

        int sum = 0;
        foreach (int cnt in numlist)
        {
            sum = sum + cnt;
        }

        Console.WriteLine("Sum is {0}", sum);
    }
}
```

Input Nil

### Output

There are 3 numbers
Their sum is 60
There are 5 numbers
Their sum is 150

## 7.4 Recursive Method Call

### Concept

- 1. A method can call itself. This is known as **recursion**.

### Explanation

- 2. Recursion, in mathematics and computer science, is a way of defining methods in which the method being defined is applied within its own definition.
- 3. In other words, a recursive method calls itself to do its job.
- 4. Recursion is a widely used approach to solve many programming tasks.

### Example

```
// Illustration of recursion that calculates factorial of a given number.
using System;

namespace
{
class NumberManipulatorClass
{
public int factorial(int num)
{
/* local variable declaration */
int result;
if (num == 1)
{
return 1;
}
else
{
result = factorial(num - 1) * num;
return result;
}
}

static void Main(string[] args)
{
NumberManipulator n = new NumberManipulator();
//calling the factorial method
Console.WriteLine("Factorial of 6 is: {0}", n.factorial(6));
Console.WriteLine("Factorial of 7 is: {0}", n.factorial(7));
Console.WriteLine("Factorial of 8 is: {0}", n.factorial(8));
Console.ReadLine();
}
}
}
```

When the above code is compiled and executed, it produces the following result :

```
Factorial of 6 is: 720
Factorial of 7 is: 5040
Factorial of 8 is: 40320
```

## 7.5 Naming the method (Nomenclature for method)

7.5.1. The name of a method primarily follows the rules defined for names of variables.
Refer (Chapter 2 - section 2.6)

7.5.2. Besides those rules, following are some suggestions for naming the methods.

- 2.1 If the name of a method is in one word, the first letter will be in uppercase
- 2.2 If the name of a method is a combination of words, the first letter of each word will be in uppercase
- 2.3 Because a method is an action, generally method name should be a verb.

7.5.3 The method names are verbs or verbs followed by adjectives or nouns. Each subsequent word starts with an uppercase character. The following are typical names of methods in C#:

- Execute
- FindRollNo
- SetName
- GetName
- CheckIfValid

## 8. The Main - Main method (public static void Main(String[] args))

8.1 There is at least one method inside C# class which is main where the execution of program starts. It is the main entry point of program that executes all the objects and invokes method to execute. There can be only one Main method in C#.

8.2 Default implementation of the Main() method is of type void. Another way to implement the Main() method is to make it return an integer. The rule is the same as for any method of type int. The Main() function can return any type of integer as long as it is a valid integer.

8.3 The Main method in C# is always declared as static because it has to be called before creation of any object or before calling any other method in the program. The Main method instantiate other objects and variables but there is no method that can instantiate main method in C#. On other hand, the main method doesn't accept parameter from any other method. It only takes parameter as argument via command line argument.

8.4 The Main method can have a parameter and these parameters are known as zero-indexed command line argument.

## 9. Method scope

### Concept

- 1. A variable declared inside a method has a method scope.

### Explanation

- 2. The scope of a name is the region of program text within which it is possible to refer to the entity declared by the name without the qualification of the name.
- 3. A variable which is declared inside a method has a method scope. It is also called a local scope.
- 4. The variable is valid only in this particular method.

### Example

```csharp
//Illustration of understanding method scope

using System;

public class DemoMethodScope
{
    int no = 1;

    public void exec1()
    {
        // no is class level variable and accessed using this reference
        // no is a instance variable

        Console.WriteLine(this.no);
        Console.WriteLine(no);
    }

    public void exec2()
    {
        int num = 5;

        Console.WriteLine(no); // variable no has class level scope.
        Console.WriteLine(num); // variable num has scope method exec2.
    }
}

public class TestMethodScope
{
    static void Main()
    {
        DemoMethodScope DMS = new DemoMethodScope();
    }
}
DMS.exec1();
DMS.exec2();
}
```

Input nil

### Output

```
1
1
1
5
```

5. A variable defined inside a method has a local/method scope. If a local variable has the same name as an instance variable, it shadows the instance variable. The class variable is still accessible inside the method by using the ‘this’ keyword.

### Example

```
//Illustration of use of this to resolve scope
using System;

public class TestScope
{
    int n = 100;

    public void exec()
    {
        int n = 300;

        Console.WriteLine(this.n);
        Console.WriteLine(n);
    }
}

public class DemoShadowing
{
    static void Main()
    {
        TestScope ts = new TestScope();
        ts.exec();
    }
}
```

In the preceding example, variable n is declared twice, outside the exec() method and inside the exec() method. Both variables have the same name, but they do not conflict because they live in different scopes.

```
Console.WriteLine(this.n);
Console.WriteLine(n);
```

The variables are accessed differently. The variable n defined inside the method, also called the local variable, is simply accessed by its name. The instance variable can be referred by using the this keyword.

Input Nil

### Output

100
300

## 10. this reference

- 10.1 The this keyword is used to refer to the current instance of the class.
- 10.2 It can be used to access members from within the constructors and instance methods.
- 10.3 The naming conflicts can be eliminated using this reference. They cannot be used as reference to a static field or method. They cannot be part of static class.

```
// Illustration of use of this reference.
class UseThis
{
    int no;
    public UseThis()
    {
        this.Decrease();
    }
    public void Decrease()
    {
        no--;
        this.no--;
        Console.WriteLine("The value of number is" + no);
    }
    static void Main (string [] args)
    {
        UseThis obj = new UseThis();
        obj.Decrease();
        Console.Read();
    }
}
```

Input Nil

### Output

-2  -4
