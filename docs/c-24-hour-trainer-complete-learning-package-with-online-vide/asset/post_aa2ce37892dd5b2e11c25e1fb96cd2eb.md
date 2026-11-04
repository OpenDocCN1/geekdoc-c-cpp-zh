
The <T> means the class takes one type parameter, T. Within the class's code, the type T means whatever type the program used when creating the instance of the class. For example, the following code declares a variable named rootNode that is a TreeNode that handles strings:

```
TreeNode<string> rootNode = new TreeNode<string>();
```

If you want the class to use multiple type parameters, separate them with commas. For example, suppose you want to make a Matcher class that takes two kinds of objects and matches objects in the two kinds. It might match Employee objects with Job objects to assign employees to jobs. The following code shows how you might declare the Matcher class:

```
public class Matcher<T1, T2>
{
    ...
}
```

The following code shows how you might create an instance of the class to match Employees with Jobs:

```
Matcher<Employee, Job> jobAssigner = new Matcher<Employee, Job>();
```

> NOTE Many developers use T for the name of the type in generic classes that take only one type.
> 
> If the class takes more than one type, you should use more descriptive names so it's easy to tell the types apart. For example, the generic Dictionary class has two type variables named TKey and TValue that represent the types of the keys and values that the Dictionary will hold.

Inside the class's code, you can use the types freely. For example, the following code shows more of the TreeNode class's code. A TreeNode object represents a node in a tree, with an associated piece of data attached to it. The places where the class uses the data type T are highlighted in bold.

```
class TreeNode<T>
{
    // This node's data.
    public T Data { get; set; }

    // This node's children.
    private List<TreeNode<T>> children = new List<TreeNode<T>>();

    // Constructor.
    public TreeNode(T data)
    {
        Data = data;
    }

    // Override ToString to display the data.
    public override string ToString()
    {
        if (Data == null) return "";
        return Data.ToString();
    }
    ...
}
```

Notice how the class uses the type T throughout its code. The class starts by defining a Data field of type T. This is the data (of whatever data type) associated with the node.

Each node also has a list of child nodes. To hold the right kind of TreeNode objects, the children variable is a generic List<TreeNode<T>>, meaning it can hold only TreeNode<T> objects.

The class's constructor takes a parameter of type T and saves it in the object's Data property.

To make displaying a TreeNode easier, the class overrides its ToString method so it calls the ToString method provided by the Data object. For example, if the object is a TreeNode<string>, this simply returns the string's value.

## USING GENERIC CONSTRAINTS

The previous example overrides the TreeNode class's ToString method to make it call the Data object's ToString method. Fortunately, all objects have a ToString method so you know this is possible, but what if you want to call some other method provided by the object?

For example, suppose you want to create a new instance of type T. How do you know that type T provides a constructor that takes no parameters? What if you want to compare two objects of type T to see which is greater? Or what if you want to compare two type T objects to see if they are the same (an important test for the Dictionary class)? How do you know whether two type T objects are comparable?

You can use generic constraints to require that the types used by the program meet certain criteria such as comparability or providing a parameterless constructor.

To use a generic constraint, follow the normal class declaration with the keyword where, the name of the type parameter that you want to constrain, a colon, and the constraint. Some typical constraints include:

- A class from which the type must inherit
- An interface (or interfaces) that the type must implement
- new() to indicate that the type must provide a parameterless constructor
- struct to indicate that the type must be a value type such as the built-in value types (int, bool) or a structure
- class to indicate that the type must be a reference type

Separate multiple constraints for the same type parameter with commas. If you want to constrain more than one type parameter, use a new where clause.

For example, the following code defines the generic Matcher class, which takes two generic type parameters T1 and T2. (Note that this code skips important error handling such as checking for null values to keep things simple.)

```
public class Matcher<T1, T2>
    where T1 : IComparable<T2>, new()
    where T2 : new()
{
    private void test()
    {
        T1 t1 = new T1();
        T2 t2 = new T2();
        ...

        if (t1.CompareTo(t2) < 0)
        {
            // t1 is "less than" t2.
            ...
        }

        ...
    }
}
```

The first constraint requires that type parameter T1 implement the IComparable interface for the type T2 so the code can compare T1 objects to T2 objects. The next constraint requires that the T1 type also provide a parameterless constructor. You can see that the code creates a new T1 object and uses its CompareTo method (which is defined by IComparable).

The second where clause requires that the type T2 also provide a parameterless constructor. The code needs that because it also creates a new T2 instance.

In general, you should use as few constraints as possible because that makes your generic code usable in as many circumstances as possible. If your code won't need to create new instances of a data type, don't use the new constraint. If your code won't need to compare objects, don't use the IComparable constraint.

## MAKING GENERIC METHODS

In addition to building generic classes, you can also build generic methods inside either a generic class or a regular non-generic class.

For example, suppose you want to rearrange the items in a list so the new order alternately picks items from each end of the list. If the list originally contains the numbers 1, 2, 3, 4, 5, 6, then the alternated list contains 1, 6, 2, 5, 3, 4.

The following code shows how a program could declare an Alternate method to return an alternated list. The part of the code that defines the generic parameter T is shown in bold.

```
public List<T> Alternate<T>(List<T> list)
{
    // Make a new list to hold the results.
    List<T> newList = new List<T>();
    ...
    return newList;
}
```

The Alternate method takes a generic type parameter T. It takes as a regular parameter a List that holds items of type T and it returns a new List containing items of type T.

The code creates a new List<T> to hold the results. (Note that it does not need to require the type T to have a default constructor because the code is creating a new List, not a new T.) The code then builds the new list (not shown here) and returns it.

The following code shows how a program might use this method:

```
List<string> strings = new List<string>(stringsTextBox.Text.Split(' '));
List<string> alternatedStrings = Alternate<string>(strings);
alternatedStringsTextBox.Text = string.Join(" ", alternatedStrings);
```

The first statement defines a List<string> and initializes it with the space-separated values in the TextBox named stringsTextBox.

The second statement calls Alternate<string> to create an alternated List<string>. Notice how the code uses <string> to indicate the data type that Alternate will manipulate. (This is actually optional and the program will figure out which version of Alternate to use if you omit it. However, this makes the code more explicit and may catch a bug if you try to alternate a list containing something unexpected such as Person objects.)

The third statement joins the values in the new list, separating them with spaces, and displays the result.

Generic methods can be quite useful for the same reasons that generic classes are. They allow code reuse without the extra hassle of converting values to and from the non-specific object class. They also perform type checking, so in this example, the program cannot try to alternate a List<int> by calling Alternate<string>.

## TRY IT

In this Try It, you build a generic Randomize method that randomizes an array of objects of any type. To make it easy to add the method to any project, you add the method to an ArrayMethods class. To make the method easy to use, you make it static, so the main program doesn't need to instantiate the class to use it.

## Lesson Requirements

In this lesson, you:

- Start a new project and give it an ArrayMethods class.
- Create a generic Randomize method with one generic type parameter T. The method should take as a parameter an array of T and randomize the items it contains.
- Make the main program test the method.
