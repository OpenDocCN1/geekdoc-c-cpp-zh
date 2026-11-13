# FIGURE 10.9 The Animal Guessing Program

# A Program

```
// FILE: animal.cxx
// This animal guessing program illustrates the use of the binary tree node class.

#include <cstdlib>    // Provides EXIT_SUCCESS
#include <iostream>   // Provides cout
#include <string>     // Provides string class
#include "bintree.h"  // Provides the binary tree node class
#include "usefull.h"  // Provides eat_line, inquire (from Appendix I)
using namespace std;
using namespace main_savitch_10;  // binary_tree_node

// PROTOTYPES for functions used by this game program:
void ask_and_move(binary_tree_node<string>* &current_ptr);
// Precondition: current_ptr points to a nonleaf node in a binary taxonomy tree.
// Postcondition: The question at the current node has been asked. The current pointer has
// been shifted left (if the user answered yes) or right (for a no answer).

binary_tree_node<string>* beginning_tree( );
// Postcondition: The return value is the root pointer of a new small taxonomy tree.

void instruct( );
// Postcondition: Instructions for playing the game have been printed to the screen.

void learn(binary_tree_node<string>* leaf_ptr);
// Precondition: leaf_ptr is a pointer to a leaf in a taxonomy tree. The leaf contains a wrong
// guess that was just made.
// Postcondition: Information has been elicited from the user, and the tree has been improved.

void play(binary_tree_node<string>* current_ptr);
// Precondition: current_ptr points to the root of a binary taxonomy tree with at least two leaves.
// Postcondition: One round of the animal game has been played, and maybe the tree has
// been improved.

int main( )
{
    binary_tree_node<string> *taxonomy_root_ptr;

    instruct( );
    taxonomy_root_ptr = beginning_tree( );
    do
        play(taxonomy_root_ptr);
    while (inquire("Shall we play again"));
    cout << "Thank you for teaching me a thing or two." << endl;

    return EXIT_SUCCESS;
}
```