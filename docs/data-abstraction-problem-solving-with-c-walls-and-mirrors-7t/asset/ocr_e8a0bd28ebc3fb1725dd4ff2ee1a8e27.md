As the problem-solving process proceeds, you gradually refine the modules until eventually you implement their actions by writing code—typically, classes and their methods. Separating the purpose of a module from its implementation is known as functional (or procedural) abstraction. Once a module is written, you can use it without knowing the particulars of its algorithm as long as you have a statement of its purpose and a description of its arguments. Assuming that the module is documented properly, you can use it knowing only its specifications. You do not need to look at its implementation.

Complete specifications enable you to use a module without knowing its implementation

Functional abstraction is essential to team projects. After all, in a team situation, you have to use modules written by others, frequently without knowledge of their algorithms. Can you actually use such a module without studying its code? In fact, you do this each time you use a C++ Standard Library function, such as sqrt in the C++ math library cmath. Because sqrt is precompiled, you do not have access to its source statements. Furthermore, it may be that sqrt was written in a language other than C++! There is so much about sqrt that you do not know; yet you can use it in your program without concern, as long as you know its specifications. If you pass sqrt a floating-point expression, it will return the floating-point square root of the value of that expression. You can use sqrt even though you do not know its implementation.

Consider now a collection of data and a set of operations on the data. The operations might include ones that add new data to the collection, remove data from the collection, or search for some data. Data abstraction focuses on what operations do with the collection of data, instead of on how you implement them. The other modules of the solution “know” what operations they can perform, but they do not know how the data is stored or how the operations are performed.

Specify what a module does, not how to do it

For example, you have used an array, but have you ever stopped to think about what an array actually is? There are many pictures of arrays throughout this book. They might resemble the way a C++ array is implemented on a computer, and then again they might not. In either case, you can use an array without knowing what it “looks like”—that is, how it is implemented. Although different systems may implement arrays in different ways, the differences are transparent to the programmer.

For instance, regardless of how the array years is implemented, you can always store the value 1492 in location index of the array by using the statement

```
years[index] = 1492;
```

and later display the value by using the statement

```
cout << years[index] << endl;
```

Thus, you can use an array without knowing the details of its implementation, just as you can use the function sqrt without knowing the details of its implementation. Let’s explore this idea in more detail.

Both functional and data abstraction ask you to think “what,” not “how”

# 1.3.4 Information Hiding

As you have seen, abstraction tells you to write functional specifications for each module that describe its outside, or public, view. However, abstraction also helps you identify details that you should hide from public view—details that should not be in the specifications but rather should be private. The principle of information hiding tells you not only to hide such details within a module, but also to ensure that no other module can tamper with these hidden details.

All modules and ADTs should hide something

While writing a module’s specifications, you must identify details that you can hide within the module. The principle of information hiding involves not only hiding these details, but also making them inaccessible from outside a module. One way to understand information hiding is to imagine walls around the various tasks a program performs. These walls prevent the tasks from becoming entangled. The wall around each task prevents the other tasks from “seeing” how that task is performed.