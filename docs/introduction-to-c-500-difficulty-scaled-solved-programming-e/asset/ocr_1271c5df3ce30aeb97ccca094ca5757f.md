# 13 • Structures and Unions 385

```
for(i = 0; i < SIZE; i++)
{
    cout << "\nEnter title: ";
    getline(cin, b[i].title);

    cout << "\nEnter code: ";
    cin >> b[i].code;

    cout << "\nEnter price: ";
    cin >> b[i].prc;
    cin.get();
}
do
{
    cout << "\nEnter two numbers [1-"]" << SIZE << ": ";
    cin >> i >> j;
} while ((i == j) || i > SIZE || j >= SIZE || i < 1 || j < 1);

i--;
j--;
max_code(&b[i], &b[j], &fin);
if(fin.code != -1)
    cout << "\nNN: " << fin.title << " C: " << fin.code << " P: " << fin.prc << "\n";
else
    cout << "\nBooks have the same code: " << b[i].code << "\n";
}
return 0;
```

```
void max_code(const Book *b1, const Book *b2, Book *fin)
{
    if (b1->code > b2->code)
        *fin = b1;
    else if (b1->code < b2->code)
        *fin = b2;
    else
        fin->code = -1;
}
```

C.13.5 Define the structure Product with members: name, code, and price. Write a function that takes as parameters a vector of such structures and the code of a product. The function should check if a product in the vector has the same code and, if so, return a pointer to the respective structure, otherwise nullptr. Write a program that uses the type Product to read the data of products and store them in a vector. If the user enters a negative value for price, the insertion of data should terminate. Then, the program should read the code of a product and use the function to display the product's name and price, if found.

```
#include <iostream>
#include <string>
#include <vector>
using namespace std;
```