3. What is a yes/no question that can distinguish the right animal from the animal that was guessed? In our example, we need a question that can distinguish a kangaroo from a raccoon. The user might provide the question “Are you a marsupial?” and we’ll store this question in another local string variable called new_question.

With the three strings set, we need one more piece of information. In particular, we need to know whether the new animal answers yes or no to the question that the user has just provided. In our example, we need to know whether a raccoon answers yes or no to the question “Are you a marsupial?” Of course, a raccoon is not a marsupial, so based on this no answer, we can proceed as follows:

+   1. Copy the new question into current_ptr's data field.
+   2. Copy the guessed animal into a new leaf, which is created to be the left child of the current node.
+   3. Copy the correct new animal into a new leaf, which is created to be the right child of the current node.

In our example, these steps improve the taxonomy tree as shown here:

![](bbox=[0.25, 0.44, 0.88, 0.64])

The other possibility is that the new animal has a yes answer to the new question. For example, the question to distinguish a raccoon from a kangaroo could be “Do you have a ringed tail?” In this case, the new animal (raccoon) would be added as the left child of the new question, and the old animal (kangaroo) added on the right.

The implementation of the learn function is part of the complete animal-guessing program in Figure 10.9.

# Animal Guessing Program—Improvements

Our animal program suffers from one problem: Each time the program is executed, it starts out by knowing only four animals. An improvement will allow it to store the current taxonomy tree in a file and read that file whenever the program starts. This way the program remembers all the animals it was taught.