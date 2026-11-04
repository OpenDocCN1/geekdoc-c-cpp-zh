
```
{ get; set; }

public override string ToString()
{
    return FirstName + ", " + LastName +
        "$" + Salary;
}

public int CompareTo(Employee emp)
{
    return this.FirstName.CompareTo(emp.FirstName);
}
```

The SalaryComparer class implements the IComparer<T> interface. IComparer<T> has one method — Compare() — that you need to implement. It compares the salary of two Employee objects.

To use the SalaryComparer class, declare the SalarySorter static property within the Employee class so that you can return an instance of the SalaryComparer class:

```
public class Employee : IComparable<Employee>
{
    private class SalaryComparer : IComparer<Employee>
    {
        public int Compare(Employee e1, Employee e2)
        {
            if (e1.Salary < e2.Salary)
                return -1;
            else if (e1.Salary == e2.Salary)
                return 0;
            else
                return 1;
        }
    }

    public static IComparer<Employee> SalarySorter
    {
        get { return new SalaryComparer(); }
    }

    public string FirstName
    { get; set; }

    public string LastName
    { get; set; }

    public int Salary
    { get; set; }

    public override string ToString()
    {
        return FirstName + ", " + LastName +
            "$" + Salary;
    }
}
```

```
}
public int CompareTo(Employee emp)
{
    return this.FirstName.CompareTo(emp.FirstName);
}
```

You can now sort the Employee objects using the default, or specify the SalarySorter property:

```
employees.Sort(); //---sort using FirstName (default)---
employees.Sort(Employee.SalarySorter); //---sort using Salary---
```

To allow the Employee objects to be sorted using the LastName property, you could define another class (say LastNameComparer) that implements the IComparer<T> interface and then declare the SalarySorter static property, like this:

```
public class Employee : IComparable<Employee>
{
    private class SalaryComparer : IComparer<Employee>
    {
        public int Compare(Employee e1, Employee e2)
        {
            if (e1.Salary < e2.Salary)
                return -1;
            else if (e1.Salary == e2.Salary)
                return 0;
            else
                return 1;
        }
    }
```

```
private class LastNameComparer : IComparer<Employee>
{
    public int Compare(Employee e1, Employee e2)
    {
        return e1.LastName.CompareTo(e2.LastName);
    }
}
```

```
public static IComparer<Employee> SalarySorter
{
    get { return new SalaryComparer(); }
}
```

```
public static IComparer<Employee> LastNameSorter
{
    get { return new LastNameComparer(); }
}
```

```
public string FirstName
{ get; set; }
public string LastName
```

```
{ get; set; }

public int Salary
{ get; set; }

public override string ToString()
{
    return FirstName + ", " + LastName +
        " $" + Salary;
}

public int CompareTo(Employee emp)
{
    return this.FirstName.CompareTo(emp.FirstName);
}
}
```

You can now sort by LastName using the LastNameSorter property:

```
employees.Sort(Employee.LastNameSorter); //---sort using LastName---
```

## Dictionary

Most of you are familiar with the term dictionary — a reference book containing an alphabetical list of words with information about them. In computing, a dictionary object provides a mapping from a set of keys to a set of values. In .NET, this dictionary comes in the form of the Dictionary class (the generic equivalent is Dictionary<T,V>).

The following shows how you can create a new Dictionary object with type int to be used for the key and type String to be used for the values:

```
Dictionary<int, string> employees = new Dictionary<int, string>();
```

To add items into a Dictionary object, use the Add() method:

```
employees.Add(1001, "Margaret Anderson");
employees.Add(1002, "Howard Mark");
employees.Add(1003, "John Smith");
employees.Add(1004, "Brian Will");
```

Trying to add a key that already exists in the object produces an ArgumentException error:

```
//---ArgumentException; duplicate key---
employees.Add(1004, "Sculley Lawrence");
```

A safer way is to use the ContainsKey() method to check if the key exists before adding the new key:

```
if (!employees.ContainsKey(1005))
{
    employees.Add(1005, "Sculley Lawrence");
}
```

While having duplicate keys is not acceptable, you can have different keys with the same value:

```
employees.Add(1006, "Sculley Lawrence"); //---duplicate value is OK---
```

To retrieve items from the Dictionary object, simply specify the key:

```
Console.WriteLine(employees[1002].ToString()); //---Howard Mark---
```

When retrieving items from a Dictionary object, be certain that the key you specify is valid or you encounter a KeyNotFoundException error:

```
try
{
    //---KeyNotFoundException---
    Console.WriteLine(employees[1005].ToString());
}
catch (KeyNotFoundException ex)
{
    Console.WriteLine(ex.Message);
}
```

Rather than catching an exception when the specified key is not found, it's more efficient to use the TryGetValue() method:

```
string Emp_Name;
if (employees.TryGetValue(1005, out Emp_Name))
    Console.WriteLine(Emp_Name);
```

TryGetValue() takes in a key for the Dictionary object as well as an out parameter that will contain the associated value for the specified key. If the key specified does not exist in the Dictionary object, the out parameter (Emp_Name, in this case) contains the default value for the specified type (string in this case, hence the default value is null).

When you use the foreach statement on a Dictionary object to iterate over all the elements in it, each Dictionary object element is retrieved as a KeyValuePair object:

```
foreach (KeyValuePair<int, string> Emp in employees)
    Console.WriteLine("({0} - {1})", Emp.Key, Emp.Value);
```

Here's the output from these statements:

1001 - Margaret Anderson
1002 - Howard Mark
1003 - John Smith
1004 - Brian Will

To get all the keys in a Dictionary object, use the KeyCollection class:

```
//---get all the employee IDs---
Dictionary<int, string>.KeyCollection
    EmployeeID = employees.Keys;

foreach (int ID in EmployeeID)
    Console.WriteLine(ID);
```

## Part I: C# Fundamentals

These statements print out all the keys in the Dictionary object:

```
1001
1002
1003
1004
```

If you want all the employees’ names, you can use the ValueCollection class, like this:

```
//---get all the employee names---
Dictionary<int, string>.ValueCollection
    EmployeeNames = employees.Values;

foreach (string emp in EmployeeNames)
    Console.WriteLine(emp);
```

You can also copy all the values in a Dictionary object into an array using the ToArray() method:

```
//--extract all the values in the Dictionary object
// and copy into the array--
string[] Names = employees.Values.ToArray();
foreach (string n in Names)
    Console.WriteLine(n);
```

To remove a key from a Dictionary object, use the Remove() method, which takes the key to delete:

```
if (employees.ContainsKey(1006))
{
    employees.Remove(1006);
}
```

To sort the keys in a Dictionary object, use the SortedDictionary<K,V> class instead of the Dictionary<K,V> class:

```
SortedDictionary<int, string> employees =
    new SortedDictionary<int, string>();
```

## Stacks

A stack is a last in, first out (LIFO) data structure — the last item added to a stack is the first to be removed. Conversely, the first item added to a stack is the last to be removed.

In .NET, you can use the Stack class (or the generic equivalent of Stack<T>) to represent a stack collection. The following statement creates an instance of the Stack class of type string:

```
Stack<string> tasks = new Stack<string>();
```

To add items into the stack, use the Push() method. The following statements push four strings into the tasks stack:

```
tasks.Push("Do homework"); //---this item will be at the bottom of the stack
tasks.Push("Phone rings");
tasks.Push("Get changed");
tasks.Push("Go for movies"); //---this item will be at the top of the stack
```

To retrieve the elements from a stack, use either the Peek() method or the Pop() method. Peek() returns the object at the top of the stack without removing it. Pop() removes and returns the object at the top of the stack:

```
Console.WriteLine(tasks.Peek()); //---Go for movies---
Console.WriteLine(tasks.Pop()); //---Go for movies---
Console.WriteLine(tasks.Pop()); //---Get changed---
Console.WriteLine(tasks.Pop()); //---Phone rings---
Console.WriteLine(tasks.Pop()); //---Do homework---
```

If a stack is empty and you try to call the Pop() method, an InvalidOperationException error occurs. For that reason, it is useful to check the size of the stack by using the Count property before you perform a Pop() operation:

```
if (tasks.Count > 0)
    Console.WriteLine(tasks.Pop());
else
    Console.WriteLine("Tasks is empty");
```

To extract all the objects within a Stack object without removing the elements, use a foreach statement, like this:

```
foreach (string t in tasks)
    Console.WriteLine(t);
```

Here's what prints out:
Go for movies
Get changed
Phone rings
Do homework

## Queues

The queue is a first in, first out (FIFO) data structure. Unlike the stack, items are removed based on the sequence that they are added.

In .NET, you can use the Queue class (or the generic equivalent of Queue<T>) to represent a queue collection. The following statement creates an instance of the Queue class of type string:

```
Queue<string> tasks = new Queue<string>();
```
