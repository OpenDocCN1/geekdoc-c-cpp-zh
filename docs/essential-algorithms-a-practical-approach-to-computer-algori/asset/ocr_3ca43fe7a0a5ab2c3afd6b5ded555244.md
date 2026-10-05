# 270 Chapter 10 ■ Trees

The algorithm examines the child that should contain the new key. If that child does not exist, the algorithm creates it and stores the rest of the key and the new value in it.

If child does exist, the algorithm recursively calls itself to add the new key (minus its first letter) to that child's subtree.

A search for a value in a trie follows the same path through the tree but uses a much simpler algorithm because there fewer special cases to consider. The following pseudocode shows how a algorithm might work in a trie:

```
// Find a value in this node's subtree.
Data: FindValue(String: target_key)
// If the remaining key matches the
// remaining node key, return this node's value.
// If (target_key == RemainingKey) Then Return Value

// Search the appropriate child.
If (Children == null) Then Return null

Integer: index = target_key[0] - 'A'
If (Children[index] == null) Then Return null
Return Children[index].FindValue(target_key.Substring(1))
End FindValue
```

The algorithm first compares the target key to the node's remaining key. If these are the same, two things may have happened. First, the algorithm may have used the target key and reached a node that doesn't have a remaining value. (This happens if you search for WAN in Figure 10-22.) Second, the algorithm may have reached a node where the remaining key matches the node's remaining key. (This happens if you search for WANTED in Figure 10-22.) In either case, this code matches the target key, so the algorithm returns its value.

If the remaining key doesn't match the node's remaining key, the algorithm must search a child. If the node has no children, the target key isn't in the trie, so the algorithm returns null.

If the node has children, the algorithm calculates the index of the target key's child. If that child does not exist, the target key isn't in the trie, so the algorithm returns null.

Finally

# Summary

Trees can be useful for storing and manipulating hierarchical data. After you build a tree, you can enumerate its values in different orders and search for values within the tree.