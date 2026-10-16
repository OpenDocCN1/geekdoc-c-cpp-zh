# 16.4.2 Examples of Binary Trees

**Binary trees** are trees in which each node has at most two children. They are especially useful in modeling processes in which some experiment or test with two possible outcomes (for example, off or on, 0 or 1, false or true, down or up, yes or no) is performed repeatedly. For example, the following binary tree might be used to represent the possible outcomes of flipping a coin three times:

![](bbox=[0.12, 0.25, 0.88, 0.42])

Each path from the root to one of the leaf nodes corresponds to a particular outcome, such as HTH (a head followed by a tail followed by another head), as highlighted in the diagram.

Similarly, a binary tree can be used in coding problems such as encoding and decoding messages transmitted in Morse code, a scheme in which characters are represented as sequences of dots and dashes, as shown in the following table:

|   |   |   |   |   |
|---|---|---|---|---|
| A | • — | J | •• — — | S | ••• | 2 | •• — — — |
| B | — ••• | K | — • — | T | — | 3 | ••• — — |
| C | — • — • | L | •• — • | U | •• — | 4 | •••• — |
| D | — •• | M | — — | V | ••• — | 5 | ••••• |
| E | • | N | — • | W | • — — | 6 | — •••• |
| F | •• — • | O | — — — | X | — •• — | 7 | — — ••• |
| G | — — • | P | • — — • | Y | — • — — | 8 | — — — •• |
| H | •••• | Q | — — • — | Z | — — •• | 9 | — — — — • |
| I | •• | R | • — • | 1 | • — — — — | 0 | — — — — — |

In this case, the nodes represent the characters and each link from a node to its children is labeled with a dot or a dash, according to whether it leads to a left child or to a right child, respectively. Thus, part of the tree for Morse code is

![](bbox=[0.3, 0.88, 0.7, 0.95])

The sequence of dots and dashes labeling a path from the root to a particular node corresponds to the Morse code for that character; for example, •• is the code for I, and — • is the code for N.