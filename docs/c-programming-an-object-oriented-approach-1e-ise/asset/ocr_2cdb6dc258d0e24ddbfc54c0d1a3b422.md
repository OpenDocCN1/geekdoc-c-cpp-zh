# ### 11.1.3 More about Public Inheritance

In this section we discuss additional issues about public inheritance.

# ### Protected Members

So far we have only discussed the private and the public members in a class. C++ also defines another specifier for a member, **protected**. A protected member acts like a private member in the base class (or when there is no derivation). When we extend a class, then the role of a protected member manifests itself. A protected member is accessible in the derived class and all classes derived from the derived class. In other words, a protected member is inherited like a private member, but it is not hidden in the derived class. The functions defined in the derived class can easily access a protected member without having to call a function inherited from the base class. Figure 11.13 shows the difference.

Figure 11.13 shows two cases. In the first case, we have only one private data member and one public member function. When we use derivation, the private member **x** is hidden. Although the function *set (x)* is public and seen in the derived class, it cannot be called directly because the parameter **x** cannot be seen. We need to create another function, with another dummy variable **y** to access **x**, as shown below:

```
```cpp
void Derived :: set (int y)
{
    Base :: set (y);          // Calling the inherited function
}
```
```

If we have defined the data member as protected, it is seen in the derived class and we can use *set (x)* directly without having to create another function with a dummy variable. The question is which approach we should take: using private data members or the protected data members. We discuss the advantage and disadvantage of both approaches next.

**Using Private Data Members**  Using private data members enforces the concept of encapsulation. As we discussed in previous chapters, encapsulation means hiding the data.

![](bbox=[0.314, 0.695, 0.845, 0.908])

**Figure 11.13**  Private versus protected member