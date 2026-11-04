creates a new object of an *anonymous type* (a type with no name), which the compiler generates for you, based on the properties listed in the curly braces {}. In this case, each new object of the anonymous type is initialized with the FirstName and LastName values from the corresponding Employee object. These selected properties can then be accessed when iterating over the results. Implicitly typed local variables allow you to use *anonymous types* because you do not have to explicitly state the type when declaring such variables.

When the compiler creates an anonymous type, it automatically generates a ToString method that returns a string representation of the object. You can see this in the program's output—it consists of the property names and their values, enclosed in braces. Anonymous types are discussed more in Chapter 20.

# Projections

The query in lines 74–75 is an example of a *projection*, which transforms an object into a new form. In this case, the transformation creates new objects containing only the FirstName and LastName properties, but projections also can manipulate the data. For example, a projection that includes the MonthlySalary could give all employees a 10% raise by multiplying their MonthlySalary properties by 1.1 with the expression

```
e.MonthlySalary * 1.1M
```

# Changing the Names of Properties in Anonymous Types

You can specify a new name for a selected property in an anonymous type. For example, if line 75 is written as

```
new {FirstName = e.FirstName, Last = e.LastName}
```

the anonymous type would have properties named First and Last, rather than FirstName and LastName. If you don't specify a new name, the property's original name is used.

# 9.4 Introduction to Collections

The .NET Framework Class Library provides several classes, called *collections*, used to store groups of related objects. These classes provide efficient methods that organize, store and retrieve your data *without* requiring knowledge of how the data is being stored. This reduces app development time.

You've used arrays to store sequences of objects. Arrays do not automatically change their size at execution time to accommodate additional elements—you must do so manually by creating a new array or by using the Array class's Resize method.

# 9.4.1 List<T> Collection

The generic collection class List<T> (from namespace System.Collections.Generic) provides a convenient solution to this problem. The T is a placeholder—when declaring a new List, replace it with the type of elements that you want the List to hold. This is similar to specifying the type when declaring an array. For example,

```
List<int> intList;
```

declares intList as a List collection that can store only int values, and

```
List<string> stringList;
```