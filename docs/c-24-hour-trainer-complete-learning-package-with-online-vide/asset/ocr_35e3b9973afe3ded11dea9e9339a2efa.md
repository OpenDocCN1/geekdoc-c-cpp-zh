The <T> means the class takes one type parameter, T. Within the class's code, the type T means whatever type the program used when creating the instance of the class. For example, the following code declares a variable named rootNode that is a TreeNode that handles strings:

```
```
TreeNode<string> rootNode = new TreeNode<string>();
```
```

If you want the class to use multiple type parameters, separate them with commas. For example, suppose you want to make a Matcher class that takes two kinds of objects and matches objects in the two kinds. It might match Employee objects with Job objects to assign employees to jobs. The following code shows how you might declare the Matcher class:

```
```
public class Matcher<T1, T2>
{
    ...
}
```
```

The following code shows how you might create an instance of the class to match Employees with Jobs:

```
```
Matcher<Employee, Job> jobAssigner = new Matcher<Employee, Job>();
```
```

> NOTE Many developers use T for the name of the type in generic classes that take only one type.
> 
> If the class takes more than one type, you should use more descriptive names so it's easy to tell the types apart. For example, the generic Dictionary class has two type variables named TKey and TValue that represent the types of the keys and values that the Dictionary will hold.

Inside the class's code, you can use the types freely. For example, the following code shows more of the TreeNode class's code. A TreeNode object represents a node in a tree, with an associated piece of data attached to it. The places where the class uses the data type T are highlighted in bold.

```
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
```
```