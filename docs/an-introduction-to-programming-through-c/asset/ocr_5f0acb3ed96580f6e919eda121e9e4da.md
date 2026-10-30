```
Node::Node(int v){
    value = v;
}
```

This sets the value member to the given value, but does nothing to the other members lhs, rhs. Is this OK? If nothing is specified, then these members will be initialized by their default constructors. But the default constructor for Set causes the member proot to be set to NULL. So the members lhs, rhs would indeed get initialized correctly.

Now we come to insertion. We will implement insertion by a function insert taking the element to be inserted as the argument. The code is recursive and follows our discussion.

```
void Set::insert(int elt){
    if(proot == NULL){proot = new node(elt);}
    else{
        if(elt == proot->value) return;    // no need to insert again.
        if(elt < proot->value) proot->left.insert(elt);
        else proot->right.insert(elt);
    }
}
```

If our set is empty, then proot will be NULL. So in this case, we will insert a node containing the new element. This is what the first statement does. If the set is not empty, then proot must be non NULL, and in this case we will come to the second line of the function. We will check if the value at the root is equal to the element being inserted, if so, we do nothing, there is no need to insert the same element again. But if the value being inserted is smaller, then we will insert into the left subtree. Similarly for the right.

The exercises ask you to define other operations, e.g. printing the set. As you might guess, most operations on trees can be naturally tackled using recursion.

# 22.2.4 A note about organizing the program

Note that our definition of Node refers to the definition of Set, and vice versa. Which one must preced the other? The definition of Set only refers to a pointer to Node. Hence we can define that after putting a forward reference to Node. The definition of Node however mentions a member of type Set. Hence it must come after the definition of Set. The implementation of the member functions in Set can come any place following the definition of Set.

# 22.2.5 On the efficiency of search trees

We first observe that there can be many binary search trees that contain a given set of numbers. Figure 22.5 give two additional trees which contain the same numbers as Figure 22.4(a).

There can be other trees also, in fact you should be able to prove that a set with 5 elements can be represented by 42 trees. Clearly, the time required to answer membership queries will depend upon which of these 42 trees has arisen during the execution.