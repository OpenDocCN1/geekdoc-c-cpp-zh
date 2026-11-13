# specification of the ask_and_move function

```
```cpp
void ask_and_move(binary_tree_node<string>*& current_ptr);
// Precondition: current_ptr points to a nonleaf node in a binary taxonomy
// tree.
// Postcondition: The question at the current node has been asked. The
// current pointer has been shifted left (if the user answered yes) or right
// (for a no answer).
```
```

The second important function used by play is called learn. The learn function is used after the game reaches a leaf and the animal at the leaf is wrong. The function elicits information from the user and thereby improves the tree, as specified here:

# specification of the learn function

```
```cpp
void learn(binary_tree_node<string>* Leaf_ptr);
// Precondition: leaf_ptr is a pointer to a leaf in a taxonomy tree.
// This leaf contains a wrong guess that was just made.
// Postcondition: Information has been elicited from the user,
// and the tree has been improved.
```
```

Using the two functions, the implementation of play is relatively short, as shown here:

```
```cpp
void play(binary_tree_node<string>* current_ptr)
// Precondition: current_ptr points to the root of a binary taxonomy tree
// with at least two leaves.
// Postcondition: One round of the animal game has been played,
// and maybe the tree has been improved.
{
    cout << "Think of an animal, then press the return key.";
    eat_line();
    while (!current_ptr->is_leaf())
        ask_and_move(current_ptr);
    cout << ("My guess is " + current_ptr->data() + ". ");
    if (inquire("Am I right?"))
        learn(current_ptr);
    else
        cout << "I knew it all along!" << endl;
}
```
```

Within this implementation we used the inquire function to ask the question "Am I right?". A function named eat_line is also used to read and throw away any characters up to the next newline character. Both of these functions are part of our toolkit of useful functions (see Appendix I). So what's left to do? Implement the two functions ask_and_move and learn, which we'll do now.