```
Greetings.Remove(2, 3); // produces "Weme"
Greetings.Insert(2, 'co'); // produces "Wecome"
Greetings.Replace('c', 's'); // produces "Wesome"
Message = Greetings.ToString();
}
}
```

# 6.6 Tuple

Tuple is a data structure which consists of the multiple parts. A C# tuple is a data structure that provides an easy way to represent a single set of data that has sequence of elements of different data types. The System.Tuple class provides static methods to create tuple objects. The Tuple<T> class was introduced in .NET Framework 4.0.

Tuples allow to,

+   - Represent multiple data into single data set.
+   - Create, access, and manipulate a data set.
+   - Return a data set from a method without using out parameter.
+   - Pass multiple values to a method through a single parameter.
+   - Can store duplicate values.

# Create and Access Tuples

Using Tuple<> class constructor or the "Create" method tuple can be created. The tuple is a set of 3 data types including two strings and one int that represents an author's name, book title, and year of publication

```
// Creating a 3-tuple that is tuple having 3 elements using constructor.
var customer = new Tuple<string, string, int>("Ravindra", "Pune", 15820);
//Display customer info
System.Console.WriteLine("Customer {0} living in {1} has {2} Account Number ", customer.Item1, customer.Item2, customer.Item3);

// Creating a 5-tuple using the static "Create" method.
// The tuple is a set of 5 data types including three strings, one int, and one double data type.
var pubCustomer = Tuple.Create("Ravindra", "Pune", "Saving", 15820, 20150000);
System.Console.WriteLine("Customer {0} living in {1} has {2} Account Numbered {3} has Balance {4}", customer.Item1, customer.Item2, customer.Item3, customer.Item4, customer.Item5);
```