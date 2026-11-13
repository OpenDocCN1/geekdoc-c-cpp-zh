```
struct TreeNode
{
   Object element;
   TreeNode *firstChild;
   TreeNode *nextSibling;
};
```

# Figure 4.3 Node declarations for trees

![](bbox=[0.07, 0.26, 0.78, 0.42])

# Figure 4.4 First child/next sibling representation of the tree shown in Figure 4.2

structure, because there would be too much wasted space. The solution is simple: Keep the children of each node in a linked list of tree nodes. The declaration in Figure 4.3 is typical.

Figure 4.4 shows how a tree might be represented in this implementation. Horizontal arrows that point downward are firstChild links. Arrows that go left to right are nextSibling links. Null links are not drawn, because there are too many.

In the tree of Figure 4.4, node E has both a link to a sibling (F) and a link to a child (I), while some nodes have neither.

# 4.1.2 Tree Traversals with an Application

There are many applications for trees. One of the popular uses is the directory structure in many common operating systems, including unix and dos. Figure 4.5 is a typical directory in the unix file system.

The root of this directory is /usr. (The asterisk next to the name indicates that /usr is itself a directory) /usr has three children, mark, alex, and bill, which are themselves directories. Thus, /usr contains three directories and no regular files. The filename /usr/mark/book/ch1.r is obtained by following the leftmost child three times. Each / after the first indicates an edge; the result is the full pathname. This hierarchical file system is very popular because it allows users to organize their data logically. Furthermore, two files in different directories can share the same name, because they must have different paths from the root and thus have different pathnames. A directory in the unix file system is just a file with a list of all its children, so the directories are structured almost exactly in accordance