# Class Functions and Conversions

# Friend Functions

The only method you currently have for accessing and manipulating a class's private variables is through the class's member functions. You can view this arrangement as illustrated in **Figure 11.4a**. At times, however, providing access to selected nonmember member functions is useful.

![](bbox=[0.403, 0.227, 0.586, 0.363])

**Figure 11.4a** Direct access provided to member functions

The procedure for providing this external access is simple: The class maintains an approved list of nonmember functions that are granted the same privileges as its member functions. The nonmember functions in the list are called **friend functions**, and the list is referred to as a **friends list**.

Figure 11.4b shows using a friends list for nonmember access. Any function attempting to access an object's private variables is first checked against the friends list: If the function is on the list, access is approved; otherwise, access is denied.

![](bbox=[0.298, 0.547, 0.701, 0.712])

**Figure 11.4b** Access provided to nonmember functions

From a coding standpoint, the friends list is simply a series of friend prototype declarations preceded by the keyword friend and included in the class declaration section. For example, if `addreal()` and `addimag()` functions are to be allowed access private members of the Complex class, the following prototypes must be included in Complex's class declaration section:

```
friend double addreal(Complex&, Complex&);
friend double addimag(Complex&, Complex&);
```