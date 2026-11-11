In Listing 17 the `*=`, `+=`, and `-=` arithmetic assignment operators have been used. The x, y, and z variables are declared in the program and initialized with the values 10, 8, 9, respectively. Then, the `*=2` arithmetic assignment operator is used with the x variable to multiply the value of x by 2. Similarly, the `+=` and `-=` arithmetic assignment operators are used with the y and z variables to add to and subtract from 2 in the respective variables.

# TEST YOUR KNOWLEDGE

Q11. Create a program to implement the `*=` and `+=` Arithmetic assignment operators.\
Ans.

```
```cpp
#include <iostream.h>

int main()
{
    int num=4;
    num *=4;

    cout << "Value of num after applying *4 is = " << num << endl;
    num +=4;
    cout << "Value of num after applying +4 is = " << num << endl;

    return 0;
}
```
```

**Output:**

```
```text
Value of num after applying *4 is = 16
Value of num after applying +4 is = 20
```
```

# Relational Operator

Relational operators are used to create expressions that evaluate to true or false. and you can use those expressions in conditional statements, such as the if statement or as the test expressions in the loop statements. Table 9 lists the relational operators present in C++:

**Table 9: Relational operator**

| Operator | Meaning | Associativity |
|---|---|---|
| `>` | Greater than | Left to right |
| `<` | Less than | Left to right |
| `>=` | Greater than equal to | Left to right |
| `<=` | Less than equal to | Left to right |