**Table 9.2** The address expression

| Group | Name | Operator | Expression | Pred | Assoc |
|---|---|---|---|---|---|
| Unary | address-of<br>indirection | &<br>* | &lvalue<br>* pointer | 17 | ← |

![](bbox=[0.33, 0.21, 0.72, 0.35])

Figure 9.10 shows how these two operators are used. The address-of operator takes a variable and returns its address; the indirection operator takes an address and returns the value of the corresponding pointed variable.

C++ uses the ampersand and the asterisk symbols for three purposes as shown in Table 9.3.

The **ampersand symbol** is used to define a reference type. It can also be used as a unary operator to get the address of a variable. It is also used as a binary bitwise AND operator (discussed in Appendix C). When it is used to define a reference type, it is put after the type (int&). When it is used to get the address of a variable, it is put before the variable name (&score). When it is used as a binary operator, it is used between the two operands.

The asterisk symbol can also be used in three situations: as a pointer type, as a unary operator to get the value of a pointed variable, and as a binary multiplication operator. When it is used to define a pointer type, it is put after the type (int*). When it is used to indirectly access a value, it is put before the pointer (*pScore). When it is used as a binary operator, it is used between the two operands.

# ### 9.2.3 Retrieving Value

After the pointer relationship is established, we can retrieve the value stored in the memory location either through the data variable or pointer variable.

**EXAMPLE 9.14**

In this example we write a simple program that accesses the values of a data variable directly and indirectly (Program 9.5).

**Table 9.3** Uses of ampersand and asterisk operators

| Symbol | Type definition | Unary operator | Binary operator |
|---|---|---|---|
| & | type& | &variable | x & y |
| * | type* | *pointer | x * y |