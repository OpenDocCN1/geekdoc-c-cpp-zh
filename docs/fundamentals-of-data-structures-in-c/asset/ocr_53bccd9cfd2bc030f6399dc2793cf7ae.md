the exponent value of a polynomial. The link field contains the address of the next term in the polynomial. The representation of polynomial in a singly linked list is shown in Fig. 3.16. The representation of a polynomial using a singly linked list is shown in Fig. 3.17.

![](bbox=[0.23, 0.15, 0.58, 0.22])

Fig. 3.16 : Representation of a polynomial node.

![](bbox=[0.08, 0.22, 0.9, 0.32])

Fig. 3.17 : Representation of a polynomial using singly linked list.

Creating a polynomial using a singly linked list starts with creating a node. Sufficient memory has to be allocated for creating a node. The information is stored in the memory, allocated by using the malloc() function of type node. In Program 3.7 the function getNode() is used for creating a node. After allocating memory for the structure of type poly, the information for the terms (i.e., coef and exp) has to be read from the user. In Program 3.7 the function readNode(), is used for reading details for the node from the user.

```
```
Algorithm for Declaration of Structure Poly
Struct POLY
COEF : FLOAT
EXP : INTEGER
NEXT : Link Field (Address of next Struct POLY)
End Struct
```
```

```
```
Algorithm for Allocating Memory for the New Node
GETNODE()
SIZE : INTEGER; NEWNODE : POLY
Step 1 : Set SIZE = get the size of the NODE
Step 2 : Set NEWNODE = Allocate space in memory for the size of SIZE and return the initial address
Step 3 : Return NEWNODE
End GETNODE()
```
```

```
```
Algorithm for Reading the Content for the New Node (Coefficient, Exponent)
READNODE(NEWNODE : NODE)
Step 1 : Read, NEWNODE ->> COEF
Step 2 : Read, NEWNODE ->> EXP
Step 3 : Set NEWNODE ->> NEXT = NULL
Step 4 : Return
End READNODE()
```
```