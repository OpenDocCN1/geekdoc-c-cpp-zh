A viable approach is to modify the tree type into a zipper. Section 5.6 implemented a zipper to navigate lists leftward and rightward. The same idea can be used to move up and down a tree.⁹ Zippers are immutable. A tree zipper combines a subtree with the sequence of steps that led to that subtree. Those steps can be reapplied, in reverse order, to go up. In contrast to returning to an existing tree, applying a step builds a new tree, which contains updated subtrees that reflect modifications to the file system. In the preceding code, the call to nav changes the type of the file system from a tree to a tree zipper, which implements navigation via its up and down methods. The final call to dir brings you back to a regular tree.

To go down a subdirectory, you create a step that contains the name of the parent directory, as well as a list of all the other nodes in that directory. For instance, going down into Dir1 in the file system from Figure 11.1 returns the subtree rooted at Dir1 but also creates a step that contains the name Root and a list of subtrees other than Dir1:

![](bbox=[0.22, 0.38, 0.73, 0.52])

You can see that from the subtree (labeled 3), the step name (labeled 1), and the step trees (labeled 2a and 2b), the previous tree can be reconstructed to go up. If the subtree has been changed—that is, replaced with a different tree—going up by reassembling will produce a different tree (same 1 and 2 parts, but a different subtree 3).

The zipper is implemented in a class DirNav:

```
Scala
final class DirNav (val dir: Dir, steps: List[(String, List[Node])]):
...
```

A zipper consists of a current directory (dir) and a list of down steps that led to it (steps). Each step is a pair that contains the name of the parent node as a String, and a list of the siblings of the current directory, of type List[Node]. The list of steps is empty when the current directory is the root of the file system.

The zipper implements two methods up and down. To move down to a subdirectory, method down produces the same subdirectory as the earlier cd method, but adds a step to the list of steps so the downward move can be reversed by method up to go back up:

⁹This section considers only up and down movements. A more complex zipper can be written to move left and right among siblings.