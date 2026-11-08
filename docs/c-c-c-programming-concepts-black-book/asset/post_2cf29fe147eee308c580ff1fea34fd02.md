
## Chapter 18

In the preceding code, we have defined an indexer that takes two strings, data and replacementData, as its arguments and replaces a string with replacementData if the string matches with data. In the Main() method, we have declared the indexer as emp["USA", "United State Of America"] = "Empty". This in turn calls the set accessor that tries to find the array element that contains the value USA. If it finds one, then USA will be replaced by United State of America. The output of the preceding code is given as follows:

```text
Employee[0]: John
Employee[1]: United State of America
Employee[2]: Software Engineer
Employee[3]: 12345
Employee[4]: Developer
```

Let’s now learn how to refer a method.

### Defining Delegates

Delegate is a C# element using which we can refer a method. This is similar to a function pointer that we have already learned in C++. However, a delegate provides type safety; thereby, making it different from a function pointer in C++.

Now, a question arises as why we need delegates in a C# program. Consider a program where we want to refer different methods, which have similar argument types, and whose return patterns are same. In this case, we can use delegates to perform the functionality. In addition, if we want to develop a general algorithm that can be applied for all the data types without writing separate methods for each data type, then we can use delegates for this purpose. Therefore, delegates provide more flexibility in a program to implement any functionality. While using delegates, we need to consider the following points:

- Methods only need to be matched with the argument types and return types of the delegate
- Delegate allows methods to be passed as a parameter

Delegates are defined at the beginning of the class definition using the delegate keyword. In addition, they must have their delegate handler methods defined in the program. Delegate handler methods are nothing but the methods that matches the argument type and return type of the delegate. Let’s demonstrate the functionality of delegates in Listing 18.15:

**Listing 18.15:** Showing an Example of Delegates

```csharp
using System;
//Defining Delegate
public delegate long Calculator(long item1, long item2);
class Program
{
    public static void Main()
    {
        Items items = new Items(6, 3);
        //Initializing the delegates
        Calculator addition = new Calculator(items.Addition);
        Calculator subtraction = new Calculator(items.Subtraction);
        Calculator multiplication = new Calculator(items.Multiplication);
        Calculator division = new Calculator(items.Division);
        //calling the delegate handler methods using the instance of
        //the delegate
        Console.WriteLine("The result of addition is: "
                          + addition(items.item1, items.item2));
        Console.WriteLine("The result of subtraction is:"
                          + subtraction(items.item1, items.item2));
        Console.WriteLine("The result of multiplication is:"
                          + multiplication(items.item1, items.item2));
        Console.WriteLine("The result of division is: "
                          + division(items.item1, items.item2));
    }
}
class Items
{
    public long item1;
    public long item2;
    public Items(long item1, long item2)
    {
        this.item1 = item1;
        this.item2 = item2;
    }
    //Defining the delegate handler
    public long Addition(long item1, long item2)
    {
        return item1 + item2;
    }
    public long Subtraction(long item1, long item2)
    {
        return item1 - item2;
    }
    public long Multiplication(long item1, long item2)
    {
        return item1 * item2;
    }
    public long Division(long item1, long item2)
    {
        return item1 / item2;
    }
}
```

In Listing 18.15, we have defined a delegate named Calculator. In addition, we have defined a class named Items that holds the delegate handler methods or the method to which the delegate will be assigned. These methods are Addition, Subtraction, Multiplication, and Division. In the Main() method, we have first instantiated an object of the Items class and then instantiated the four objects of Calculator delegate for four different delegate handler methods. At last, we have referenced the respective methods by passing the values using the objects. The output of the preceding code is given as follows:

```text
The result of addition is: 9
The result of subtraction is: 3
The result of multiplication is: 18
The result of division is: 2
```

Let's consider another example of delegates where we compare the name and employee ID of an employee and print the result on the console, as shown in Listing 18.16:

**Listing 18.16: Showing another Example of Delegates**

```csharp
using System;
//Defining delegate
public delegate void DelComparisonMethod(object obj1, object obj2);
public class DelExample
{
    Employee[] employee = new Employee[2];
    public DelExample()
    {
        employee[0] = new Employee(1001, "John Mathew", "USA");
        employee[1] = new Employee(1005, "George Mallory", "UK");
    }

    public static void Main()
    {
        DelExample delExam = new DelExample();
        //Instantiating two delegates
        DelComparisonMethod delCompName =
            new DelComparisonMethod(Employee.CompareEmpName);
        DelComparisonMethod delCompID =
            new DelComparisonMethod(Employee.CompareEmpID);
        //calling the delegate handler methods using the delegate
        //instance
        delCompName(delExam.employee[0], delExam.employee[1]);
        delCompID(delExam.employee[0], delExam.employee[1]);
    }
}
public class Employee
{
    public int emp_ID;
    public string name;
    public string address;
    public Employee(int empID, string empName, string empAddress)
    {
        this.emp_ID = empID;
        this.name = empName;
        this.address = empAddress;
    }
    //defining the delegate handler method or the method which will
    //be assigned to delegate
    public static void CompareEmpName(object name1, object name2)
    {
        string name_1 = ((Employee)name1).name;
        string name_2 = ((Employee)name2).name;
        if(String.Compare(name_1, name_2) > 0)
        {
            Console.WriteLine(name_2 + " comes before " + name_1);
        }
        else
        {
            Console.WriteLine(name_2 + " comes after " + name_1);
        }
    }
    public static void CompareEmpID(object ID1, object ID2)
    {
        int ID_1 = ((Employee)ID1).emp_ID;
        int ID_2 = ((Employee)ID2).emp_ID;
        if(ID_1 > ID_2)
        {
            Console.WriteLine(ID_1 + " is greater than " + ID_2);
        }
        else
        {
            Console.WriteLine(ID_1 + " is either equal to or smaller than " + ID_2);
        }
    }
}
```

In the preceding code, we have defined the delegate named DelComparisonMethod that takes two objects as arguments and returns a bool type. Then, we have written a class Employee that has emp ID, name, and address as its member variables. In addition, it has two delegate handler methods whose return type and argument type are same as the delegate. These two delegate handler methods operate on two different data types; and therefore, impose the flexibility. The two handler methods compare the emp_ID and name and depending on the result, return either true or false. The preceding code also has a class named DelExample that holds the Main() method. This class has first instantiated the two instances of the Employee class and then saved them in an Employee array. Within the Main() method, we have first created an object of the DelExample class and then created the two objects of delegate methods for each delegate handler method. The output of the preceding code is given as follows:

```text
George Mallory comes before John Mathew
1001 is either equal to or smaller than 1005
```

### Defining Events

In traditional console applications, there were no options for a developer to write a code that can be fired on the click of some keys. To execute an event on the click of a key, we need to follow certain steps of execution manually. However, nowadays, most of the applications are event driven. Therefore, C# allows a developer to write events in a program. Event in C# is a kind of delegate that can only be invoked from within the class where the delegate is declared.

Suppose a class includes a definition of an event. It may happen that an application contains more than one class and one of the class want to use the event declared in another class. This operation can be done by using delegates. Listing 18.17 shows how an event can be used in a C# program:

**Listing 18.17: Showing an Example of Event**

```csharp
using System;
//Defining delegate
delegate void PromotedDelegate();
class Program
{
    public static void Main()
    {
        Friend f = new Friend();
        Employee e = new Employee();
        //Adding event handler to PromotedEvent event
        e.PromotedEvent += new PromotedDelegate(f.CallWhenPromoted);
        //Invoking the event
        e.Promote();
    }
}
class Employee
{
    //Defining an event
    public event PromotedDelegate PromotedEvent;
    public void Promote()
    {
        PromotedEvent();
    }
}
class Friend
{
    //This method is called when the event is fired
    public void CallWhenPromoted()
    {
        Console.WriteLine("Thanks for calling.....");
    }
}
```
