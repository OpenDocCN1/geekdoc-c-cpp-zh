...

}

Restrict the type that can be substituted for the generic type parameter

Specify a constraint by using a where clause when defining the class. For example:

Click here to view code image

```
public class Tree<TItem>
where TItem : IComparable<TItem>
{
  ...
```

Define a generic method

Define the method by using type parameters. For example:

Click here to view code image

```
static void InsertIntoTree<TItem>
(Tree<TItem> tree, params TItem[] data)
{
  ...
```

Invoke a generic method

Provide types for each of the type parameters. For example:

Click here to view code image

```
InsertIntoTree<char>(charTree, 'Z', 'X');
```

Define a covariant interface

Specify the out qualifier for covariant type parameters. Reference the covariant type parameters only as the return types from methods and not as the types for method parameters:

Click here to view code image

```
interface IRetrieveWrapper<out T>
{
  T GetData();
}
```