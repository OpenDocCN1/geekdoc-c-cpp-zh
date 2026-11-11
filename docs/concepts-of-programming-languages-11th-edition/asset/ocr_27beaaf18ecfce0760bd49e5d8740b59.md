**Figure 1.5**
Hybrid implementation system

![](bbox=[0.263, 0.07, 0.555, 0.661])

# ### 1.7.4 Preprocessors

A preprocessor is a program that processes a program just before the program is compiled. Preprocessor instructions are embedded in programs. The preprocessor is essentially a macro expander. Preprocessor instructions are commonly used to specify that the code from another file is to be included. For example, the C preprocessor instruction

```
```c
#include "myLib.h"
```
```

causes the preprocessor to copy the contents of myLib.h into the program at the position of the #include.

Other preprocessor instructions are used to define symbols to represent expressions. For example, one could use