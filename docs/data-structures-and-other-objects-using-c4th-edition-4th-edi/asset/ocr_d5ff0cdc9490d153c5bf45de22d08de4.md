As you might guess, the data used by the program is stored in a binary taxonomy tree, as described on page 478, with each nonleaf node containing a question. When the program begins, it will only know about four animals, and the taxonomy tree will look like this:

![](bbox=[0.26, 0.23, 0.84, 0.38])

The program maintains a root pointer that always points to the root of the binary taxonomy tree. As the game is being played, the program also maintains a second pointer called current_ptr. The current pointer starts at the root and travels down the tree according to the answers that the user provides. For example, suppose that the user answers yes to the first question “Are you a mammal?” Then the program will move its current pointer to the left subtree, as shown here:

![](bbox=[0.26, 0.49, 0.84, 0.68])

In the drawing we have hidden part of the tree to indicate that only the left subtree is now relevant to the game. The rest of the tree and the root pointer are still present, but they are not needed at this point in the game. The program continues asking questions. Each time the user answers yes to a question, the current pointer is moved left. Each no answer moves the current pointer right. This continues until the program reaches a leaf. When a leaf is reached, the program guesses that you are the animal whose name is stored at the leaf. If the leaf contains the correct animal, then all is well. But if the guess is wrong, then the program elicits information from the user, and that information is used to update the taxonomy tree.