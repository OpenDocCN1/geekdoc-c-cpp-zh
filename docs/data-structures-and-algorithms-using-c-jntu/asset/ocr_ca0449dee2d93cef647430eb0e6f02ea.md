![](bbox=[0.26, 0.08, 0.73, 0.51])

# Figure 15.3 Example of standard tries

If the pattern “BLUE” is to be searched the search starts from the root node, passes through the node “B”, “L”, “U”, and finally “E”. Because of the pattern found in the tree the standard trie returns the offset of the “B”.

The standard tries can also be called digital search trees. These tries operate at the character level or bit- level.

If any node is to inserted then find whether the root node is empty or not. If the root node is empty, then create a node and treat that node as the root node. This is done by creating a node, storing the node value in the node and inserting the node at the first level. If the node that to be inserted is already present in the tree then insert the next node.

# Disadvantages of standard tries:

+   - Uses more number of nodes than other tries (space complexity is more than that of other tries)
+   - Not suitable for matching non-word patterns, such as string with white space
+   - Can compare a single character at a time

# Node structure of a standard trie:

The structure of the node of the standard trie will have 256 symbol elements array and 256 links or branches. Each node will be capable of handling any character, printable or non-printable characters.

If the trie is limited to only upper case alphabets, the number of symbol elements will be 26 and branches or links will be 26.