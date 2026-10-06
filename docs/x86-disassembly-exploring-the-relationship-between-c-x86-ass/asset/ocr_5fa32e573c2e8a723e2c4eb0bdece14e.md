# # 20 Objects and Classes

# ## 20.1 Object-Oriented programming

**Object-Oriented** (OO) provides for us a new unit of program structure to contend with: the Object. This chapter will look at in disassembled classes from C++. This chapter will not deal directly with COM, but it will work to set a lot of the groundwork for future discussions in reversing COM components (Windows users only).

# ## 20.2 Classes

A basic class that has not inherited anything can be broken into two parts, the variables and the methods. The non-static variables are shoved into a simple data structure while the methods are compiled and called like every other function.

When you start adding in inheritance and polymorphism, things get a little more complicated. For the purposes of simplicity, the structure of an object will be described in terms of having no inheritance. At the end, however, inheritance and polymorphism will be covered.

# ### 20.2.1 Variables

All static variables defined in a class resides in the static region of memory for the entire duration of the application. Every other variable defined in the class is placed into a data structure known as an object. Typically when the constructor is called, the variables are placed into the object in sequential order, see **Figure 1.**

A:

```
class ABC123 {
public:
    int a, b, c;
    ABC123():a(1), b(2), c(3) {};
};
```

B:

| 0x00200000 | dd | 1 | int a |
| 0x00200004 | dd | 2 | int b |
| 0x00200008 | dd | 3 | int c |