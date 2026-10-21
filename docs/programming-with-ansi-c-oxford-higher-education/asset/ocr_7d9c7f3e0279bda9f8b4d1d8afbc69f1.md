```
char cName[] = "Brian Charles Lara";

// Instance 1
if(Max(i1, i2))
    cout << "i1 is bigger\n";
else
    cout << "i2 is bigger\n";

// Instance 2
if(Max(sName, sAddress))
    cout << "sName is bigger\n";
else
    cout << "sAddress is bigger\n";

// Instance 3
if(Max(cName, cAddress))
    cout << "cName is bigger\n";
else
    cout << "cAddress is bigger\n";
}
```

Output
i2 is bigger
sAddress is bigger
cName is bigger

> Note Strings are compared in a lexicographical manner. Thus, West Indies is bigger than Brian Charles Lara, as 'B' appears before 'W' in the dictionary. This holds true even when the number of characters in the second string is more than that of the first one.

# How the Program Works

The output is surprising. The comparison of the two strings yields the correct output but the comparison of two character arrays does not. Why? cName and cAddress are the names of the character arrays and are pointers to the first elements of the respective array. When they both are compared, the pointer value, that is, the address is compared; so, the item defined next becomes larger. Hence, cName, which is defined after cAddress, gets a larger address value. On the contrary, the < operator is overloaded in string class, and hence the behaviour there is more meaningful. The < operator yields true if the string on the LHS is lexically smaller than that on the RHS; otherwise, it returns false.

How can this problem be solved? If there is a class, it can be solved by providing an appropriate operator overloading to eliminate this. Unfortunately, that is not possible if the type is built-in (such as C-type arrays) or if the class is defined by others (where the source code is not available to modify the class). The answer to this problem is to overload the template itself for that particular type. We will see an improved version of this program using this solution in Program 7.8.

# 7.2.6 Function Templates with Multiple Arguments

It is possible to have templates with more than one argument. Other arguments can be generic or normal. Program 7.4 is a simple search program for searching an element in the array. Here, we need to pass two arguments, the array and the element to be searched, both of which are bound to be of generic type.