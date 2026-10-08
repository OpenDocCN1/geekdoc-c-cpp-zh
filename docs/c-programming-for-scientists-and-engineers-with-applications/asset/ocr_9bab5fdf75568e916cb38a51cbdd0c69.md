# 686 Structures

```
triangle[1].p2[0] = 6.2;  triangle[1].p2[1] = 10.0; /* point(6.2,10.0) */
tangle[2].p1[0] = 6.2;  triangle[2].p1[1] = 10.0; /* point(6.25,10.0) */
tangle[2].p1[0] = 14.6;  triangle[0].p1[1] = 8.9; /* point(14.6,8.9) */
```

Each of the sides shares an endpoint with each of the other sides. Notice that a subscript must be used for each element of the array triangle and then a subscript must be used for each element of the arrays p1 and p2.

# 11.1.4 Definition of Structure Variables

Structure variables must be defined before they are used. This simply means the structure variable members must have values before they are manipulated. There are four different ways the members of a structure variable can be defined.

+   1. By initializing the members of a structure variable when the structure and variable are declared.
2. By initializing the members of a structure variable when it is declared using a named structure data type.
3. By explicit assignment of values to the members of a structure variable after it is declared using assignment statements and strcpy.
4. By data input to the members of a structure variable.

Initialization of Structure Variables Structure variables may be initialized in several ways. One way is to initialize the structure variable in a declaration of both the structure and the structure variable. The following code shows such an initialization.

```
struct gadgetpart {
    char pname[10];
    int count;
    float unitcost;
    float totalcost;
}part = {olt", 20, 0.25, 0.00};
```

Notice that the structure data type and the structure variable part are declared and the structure variable part is initialized. The member name has the string value "bolt", the member count has the value 20, the member unitcost has the