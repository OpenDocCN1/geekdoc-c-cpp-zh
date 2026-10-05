# A.5. Cscope

GIT is a cleanly designed and well-thought-out program. Although there are many facilities in GIT, GIT can be grasped easily by paying attention to its internal design. With that in mind, we mention a few points about GIT internals:

+   - GIT thinks of file as an atom. If there is a slightest change to a file, it becomes a new object as far as GIT is concerned
- As the source tree evolves, every file is stored in .git/, including older versions. The name and location of a file are obtained using its 160-bit SHA22 hash. Alternatively, GIT may compress several files into a single pack file.
- A commit is a tree-like hierarchy of files, with the working directory corresponding to one particular commit. Commit objects are also stored in .git/
- GIT thinks of commits as being organized in a directed acyclic graph. Those vertices of the directed acyclic graph, whose files may be modified to produce new commits and grow the graph, are labeled using branch names.
- When a GIT repository is cloned, it is cloned in full, including all the ancestors of a branch.

# A.5 Cscope

The cscope utility is invaluable for browsing source code. Using cscope, one can easily find the definition of a function, the places where it is called, and search for patterns inside the entire source tree. It is a search utility that predates the era of Internet search by a few decades.

Suppose the source for this book is saved in the GIT repository BOOK-SPCA. To prepare cscope database files, we may run the command

```
cscope.py BOOK-SPCA
```

in the parent directory of BOOK-SPCA; cscope.py is the following Python script, which must be on the user's path:

```
#!/usr/bin/env python
import os, sys
```