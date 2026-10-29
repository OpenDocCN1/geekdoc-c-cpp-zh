2. Obtain the source code for the PFArrayD class and the demonstration program from Displays 10.10, 10.11, and 10.10. Modify this program to use namespaces and separate compilation. Put the class definition and other function declarations in one file. Place the implementations in a separate file. Distribute the namespace definition across the two files. Place the demonstration program in a third file. To provide access to names in namespaces, you may use local using declarations such as:

```
using std::cout;
```

or use local using directives such as:

```
using namespace std;
```

inside a block, or qualify names using the names of namespaces, such as std::cout. You may not use global namespace directives such as the following which are not in a block and apply to the entire file:

```
using namespace std;
```

3. Extend the Programming Project 1 from Chapter 10 in which you implemented a two dimensional array class by placing the class definition and implementation in a namespace, then providing access to the names in the namespace. Test your code. To provide access to names in namespaces, you may use local using declarations such as

```
using std::cout;
```

or use local using directives such as:

```
using namespace std;
```

inside a block, or qualify names using the names of namespaces, such as std::cout. You may not use global namespace directives such as the following which are not in a block and apply to the entire file:

```
using namespace std;
```