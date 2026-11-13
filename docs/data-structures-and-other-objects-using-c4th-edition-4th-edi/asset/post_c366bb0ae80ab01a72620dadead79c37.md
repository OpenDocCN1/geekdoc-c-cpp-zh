
## (FIGURE 10.9 continued)

```cpp
void learn(binary_tree_node<string>* leaf_ptr)
// Library facilities used: bintree.h, iostream, string, useful.h
{
    string guess_animal; // The animal that was just guessed
    string correct_animal; // The animal that the user was thinking of
    string new_question; // A question to distinguish the two animals

    // Set strings for the guessed animal, correct animal, and a new question.
    guess_animal = leaf_ptr->data( );
    cout << "I give up. What are you? " << endl;
    getline(cin, correct_animal);
    cout << "Please type a yes/no question that will distinguish a" << endl;
    cout << correct_animal << " from a " << guess_animal << "." << endl;
    cout << "Your question: " << endl;
    getline(cin, new_question);

    // Put the new question in the current node, and add two new children.
    leaf_ptr->set_data(new_question);
    cout << "As a " << correct_animal << ", " << new_question << endl;
    if (inquire("Please answer"))
    {
        leaf_ptr->set_left( new binary_tree_node<string> (correct_animal) );
        leaf_ptr->set_right( new binary_tree_node<string> (guess_animal) );
    }
    else
    {
        leaf_ptr->set_left( new binary_tree_node<string> (guess_animal) );
        leaf_ptr->set_right( new binary_tree_node<string> (correct_animal) );
    }
}
```

```cpp
void play(binary_tree_node<string>* current_ptr)
// Library facilities used: bintree.h, iostream, string, useful.h
{
    cout << "Think of an animal, then press the return key.";
    eat_line( );

    while ( !current_ptr->is_leaf( ))
    {
        ask_and_move(current_ptr);
    }

    cout << "My guess is " << current_ptr->data( );
    if (inquire(" Am I right?"))
        learn(current_ptr);
    else
        cout << "I knew it all along!" << endl;
}
```

## Self-Test Exercises for Section 10.3

- 12. What is the base case for the recursive functions `tree_clear` and `tree_copy`?
- 13. Write a new function to compute the number of children that a node has.
- 14. Write a new function to compute the number of nodes in a binary tree. Write another function to compute the depth of a binary tree. Both functions have one argument, which is the tree's root pointer. Think recursively.

## 10.4 TREE TRAVERSALS

> And then he got up, and said: “And the only reason for making honey is so as I can eat it.” So he began to climb the tree.
> 
> He climbed and he climbed and he climbed, and as he climbed he sang a little song to himself.
> 
> A.A. MILNE
> Winnie-the-Pooh

### Traversals of Binary Trees

Programs that use tree structures often need to process all of the nodes in a tree, applying the same operation to each node. This processing is called a **traversal**. For example, suppose we have a tree where each node contains an integer, and we need to print a list of all the integers in the tree. For a binary tree, there are three common ways of doing this kind of processing: **pre-order traversal**, **in-order traversal**, and **post-order traversal**. This section defines and implements the three traversal methods for binary trees. We also implement an unusual fourth traversal method (**backward in-order traversal**), which is useful for printing a tree. We start with a description of each method.

pre-order: the root is processed prior to its two subtrees

#### Pre-order traversal.

The word “pre-order” means the root is processed previous to its two subtrees. So, a pre-order traversal has these three steps for a non-empty tree:

- 1. Process the root.
- 2. Process the nodes in the left subtree with a recursive call.
- 3. Process the nodes in the right subtree with a recursive call.

At the end of this section we’ll give an extremely general implementation of these three steps, which will allow you to do any kind of processing on each node. For now, let’s look at a simpler case, where we just want to print the contents of each node. In this case we would add this template function to the binary tree functions of Section 10.3:

```cpp
template <class Item>
void preorder_print(const binary_tree_node<Item>* node_ptr)
// Precondition: node_ptr is a pointer to a node in a binary tree (or
// node_ptr may be NULL to indicate the empty tree).
// Postcondition: If node_ptr is non-NULL, then the data of *node_ptr and
// all its descendants have been written to cout with the << operator, using
// a pre-order traversal.
// Library facilities used: cstdlib, iostream
{
    if (node_ptr != NULL)
    {
        std::cout << node_ptr->data( ) << std::endl;
        preorder_print( node_ptr->left( ) );
        preorder_print( node_ptr->right( ) );
    }
}
```

Notice how the processing of the two subtrees is accomplished with recursive calls. It's also important to see that pointers to the roots of the left and right subtrees of the original node are passed as arguments to the recursive calls.

Let's look at an execution of the pre-order traversal in more detail. We'll trace preorder_print, applied to the binary tree shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_528_0.png)

Suppose that our node_ptr points to the shaded root in the diagram. The function's first step is to print the number at the root, so after this step, the only number printed is 14 (from the root).

The function's second step makes a recursive call, with a pointer to the root node of the left subtree. In effect, the recursive call says "do a pre-order traversal of the left subtree." To illustrate that we are now doing a traversal of a subtree, we will temporarily hide everything except the left subtree, as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_529_0.png)

In this recursive call, the node_ptr points to the shaded node containing 17. The first step of the recursive call is to print the number at the node_ptr, so after that step the total output contains two numbers:

```
14
17
```

The second step of the recursive call is to make yet another recursive call, with the argument being its own node_ptr->left(). In other words, this second recursive call will begin at the shaded node containing 9 in this drawing:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_529_1.png)

We now have three function calls that are active: the original function call with the pointer to the root (containing 14), the first recursive call with a pointer to the left child of the root (containing 17), and the second recursive call with a pointer to the shaded node as shown (containing 9). This second recursive call carries out its appointed task by first printing a 9. After this, the total output consists of these three lines:

```
14
17
9
```

Once again, the function makes a recursive call. But this time the argument node_ptr->left( ) is NULL, indicating that there is no left subtree of the current node_ptr, so the function call returns. Where does it return to? It returns to the place where it was called, with the node_ptr pointing to the node with 9, and executing the code at the spot marked here with an arrow:

```
if (node_ptr != NULL)
{
    std::cout << node_ptr->data( ) << std::endl;
    preorder_print( node_ptr->left( ) );
    preorder_print( node_ptr->right( ) );
}
```

At this point in the recursive call, we have already printed the 9 and processed the empty left subtree. So the next step will make another recursive call to process the right subtree. The next step in this recursive call points to the node with 13, in this drawing:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_530_0.png)

This function call prints the number 13, so that the entire output now has four numbers:

```
14
17
9
13
```

Both the left and right subtrees are empty for the node containing 13. So the recursive calls made at this level (to process those two empty subtrees) will do no work. The recursive call, which printed 13, returns. Where do matters go from there? Can you finish tracing the pre-order traversal? By the time the last recursive call has returned, we’ve “visited” every node in the tree, and the numbers have been printed out, in this order:
