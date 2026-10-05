# C24.6 A simple way to encrypt data by XOR them with a secret key. Write a program that reads a key character and the name of a text file and encrypts it by XORing each character with the key. The encrypted characters should be stored in a second file selected by the user.

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
    int ch, key_ch;
    string fname;

    cout << "Enter input file: ";
    cin >> fname;
    ifstream fin(fname.c_str());
    if(fin.is_open() == false)
    {
        cout << "Error: Input file can't be loaded\n";
        exit(EXIT_FAILURE);
    }

    cout << "Enter output file: ";
    cin >> fname;
    ofstream fout(fname.c_str());
    if(fout.is_open() == false)
    {
        fin.close();
        cout << "Error: Output file can't be created\n";
        exit(EXIT_FAILURE);
    }

    cin.get();
    cout << "Enter key char: ";
    key_ch = cin.get();
    while (1)
    {
        ch = fin.get();
        if(!fin)
            break;
        fout << (char) (ch ^ key_ch);
    }
    fin.close();
    fout.close();
    return 0;
}
```

**Comments:** If you rerun the program and give as an input the encrypted file and the same key, the output file would be the same as the original file, because according to the Boole algebra we have: (a ^ b) b = a.

**C24.7** Define the class Country with private members: name, capital, and population. Suppose each line of the country.txt file contains the data of the respective country in the form:

name capital population