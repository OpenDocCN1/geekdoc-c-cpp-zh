```
Enter an integer (-1 to stop): 123456789
and the base to which it is to be converted: 26

aa44a1 is the base-26 representation of 123456789

Enter an integer (-1 to stop): -1
```

The convert() function in this program relies heavily on the C++ Standard Template Library's stack<T> container. We will now take a look at this container.

# 16.1.3 The stack<T> Adapter

We have already seen that the Standard Template Library provides containers such as vector<T> and list<T> for storing sequences. The designers of STL recognized that they could reuse the work they had invested in building these sequential containers to implement other containers and they did this by means of adapters that act as “wrappers” around other components, giving them new interfaces. In particular, a stack<T> container could be built as an adapter of vector<T>, list<T>, or deque<T> (described in the next section).

To illustrate, we will use the declaration of digitStack in Example 16.1:

```
stack<int> digitStack;
```

This declaration uses the default constructor in stack<T> to create digitStack and STL's default stack<T> implementation as an adapter of a deque<T>.² But if we prefer a stack<T> built using one of the other two containers, we can specify this in the declaration. For example,

```
stack<int, list<int> > intListStack;
```

builds intListStack using list<T>; and the declaration

```
stack<int, vector<int> > intVectorStack;
```

builds intVectorStack using vector<T>.

Each of these constructors builds a stack, but the underlying implementations are different. The object intListStack will be implemented using STL's linked list (and thus use memory fairly efficiently but provide slightly slower versions of push() and pop()):

> ² The default stack<T> constructor builds the stack using the deque<T> template so this declaration could also be written stack< deque<T> >.