# 9.8　Difference between Structure and Union

Union is also a template used for creating a ‘user-defined data type’ like a structure with only difference that union facilitates the programmer to create members that share a common memory space unlike structures wherein each of the members are stored in a separate memory space. The syntax of defining a union is exactly similar to that of defining a structure except the keyword `struct` is replaced by `union` as shown in the Figure 9.31.

![](bbox=[0.333, 0.262, 0.643, 0.515])

**Figure 9.31:** Syntax for creating an union

As unions facilitate sharing of memory among its members, the memory allocated for a union object will be exactly same as the memory required by the member of the biggest size defined in the union. Hence, the amount of memory for a union object is calculated as below:

```
sizeof(UnionObject) = Max (sizeof(member1), sizeof(member2) ...........
                    sizeof(memberN))
```

where union has n members defined as shown in the Figure 9.31.

This means that, we will not be able to simultaneously access and store the values of two different member variables defined inside the union. This is because, the value stored for a particular member would overwrite the value of some other member that was previously stored in the memory of the union object.

As an example, let us create a union named as Abc with members a, b, and c of type integer, float and character, respectively (Figure 9.31). The definition of the union is as in the following:

```
union Abc
{
int a;
float b;
char c;
};
```