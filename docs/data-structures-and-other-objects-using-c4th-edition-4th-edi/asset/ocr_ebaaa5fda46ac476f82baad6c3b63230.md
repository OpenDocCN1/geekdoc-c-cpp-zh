```
template <class Item>
class graph
{
public:
  ...
  Item& operator [ ] (std::size_t vertex);
  ...
```

In this definition, you can see the prototype for the overloaded subscript operator. Note that the return value is a reference. As discussed on page 318, this allows us to use the operator to actually change a label (such as the assignment statement g[3] = 42). An ordinary return value of Item would permit us to get a current value, but it would not provide any way to change a label.

The full implementation of the overloaded subscript operator is shown here:

```
template <class Item>
Item& graph<Item>::operator [ ] (std::size_t vertex)
{
  assert(vertex < size( ));
  return labels[vertex];
}
```

The return statement, return labels[vertex], indicates that any changes that the calling program makes directly on the return result will actually change the component labels[vertex] in the private member variable labels.

# A Const Version of the Subscript Operator

The subscript operator described above returns a reference to the label of the vertex, allowing the label to be changed. Therefore the operator is not a constant member function, and it cannot be used with a graph that is declared with the const keyword (such as const graph<int> g). This is similar to the data member function from our node class for linked lists (see page 320). The solution is to provide a second version of the subscript operator, which returns only a copy of the vertex's label, as shown here:

```
template <class Item>
Item graph<Item>::operator [ ] (std::size_t vertex) const
{
  assert(vertex < size( ));
  return labels[vertex];
}
```

The only difference between this and the earlier version is that the return type of the new version is Item (rather than a reference Item&). Therefore, it is not possible to use the new version to change a vertex, and the new version can be declared as a constant member function.