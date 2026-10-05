```
ifstream fin("test.dat", ios_base::in | ios_base::binary);
if(fin.is_open() == false)
{
    cout << "Error: is_open failed\n";
    exit(EXIT_FAILURE);
}
cout << "Enter virus signature " << SIZE << " integers\n";
for(i = 0; i < SIZE; i++)
{
    cout << "Enter number: " << ";";
    cin >> sign[i];
}
len = sizeof(sign);
found = 0;
back = len - sizeof(int);
while (1) {
    fin.read((char*)buf, SIZE * sizeof(int));
    if(!fin) {
        break;
    }
    if(memcmp(buf, len) == 0) {
        found = 1;
        break;
    } else {
        fin.seekg(-back, ios_base::cur); /* Go back to check the next group of five. */
    }
}
if(found == 1)
    cout << "SOS: Virus found\n";
else
    cout << "That virus signature isn't found\n";
fin.close();
return 0;
```

**C.24.12** Define the Employee structure with members: name (use an array of 100 characters), tax number, and salary. Write a program that uses this type to read the data of 100 employees and store them in an array of structures. If the user enters fin for name, the data insertion should terminate and the program should write the structures in the test.bin binary file.

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

struct Employee {
    char name[100];
    int tax_num;
    int salary;
};
```