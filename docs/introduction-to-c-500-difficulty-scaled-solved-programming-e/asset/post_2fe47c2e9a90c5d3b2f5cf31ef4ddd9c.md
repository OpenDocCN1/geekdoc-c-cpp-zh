
```cpp
#include <string>
using namespace std;

class Student {
private:
    int code;
    float grd;
    string name;
public:
    Student(int c, const string& n, float g) : code(c), name(n), grd(g) {}
    friend ostream& operator<<(ostream&, Student& s);
    friend ostream& operator<<(ostream&, const Student& s);
    void show() const { cout << "N:" << name << " C:" << code << " G:" << grd << '\n'; }
};

istream& operator>>(istream&, Student& s) {
    in >> s.name >> s.code >> s.grd;
    return in;
}

ostream& operator<<(ostream&, const Student& s) {
    out << s.name << '\t' << s.code << '\t' << s.grd << '\n';
    return out;
}

int main() {
    Student s1(1, "First", 2.5), s2(2, "Second", 7.5);

    fstream fstr("test.txt", ios_base::in | ios_base::out | ios_base::trunc);
    if(fstr.is_open() == false) {
        cout << "Error: File cannot be opened\n";
        exit(EXIT_FAILURE);
    }
    fstr << s1 << s2;
    fstr.seekg(0);
    fstr >> s1 >> s2;
    s1.show();
    s2.show();
    fstr.close();
    return 0;
}
```

**Comments:** To access the private members we declare the overloaded functions as friends. The function return references so that the << and >> operators can be used sequentially. Note that the references could be fstream, I just used the base classes to make it clearer.

**C.24** Write a program that reads continuously products’ codes and their prices and stores them in the test.txt file, as follows:

```
C101 17.5
C102 32.8
...
```

If the user enters -1 for price, the insertion of insert() should terminate. Then, the program will read a product code and search the file to find and display its price, if found.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main() 
{
    bool found;
    string code, tmp;
    double prc;

    fstream fstr("test.txt", ios_base::in | ios_base::out | ios_base::trunc);
    if(fstr.is_open() == false) {
        cout << "Error: is_open() failed\n";
        exit(EXIT_FAILURE);
    }
    while(1) {
        cout << "Enter price: ";
        cin >> prc;
        if(prc == -1) {
            break;
        }
        cin.get();
        cout << "Enter product code: ";
        getline(cin, code);
        fstr << code << ' ' << prc << '\n';
    }
    cin.get();
    cout << "Enter product code to search for: ";
    getline(cin, tmp);
    found = 0;
    fstr.seekg(0);
    while(1) {
        if(!fstr >> code >> prc) {
            break;
        }
        if(code == tmp) {
            found = 1;
            break; /* Since the product is found we can terminate the loop. */
        }
    }
    if(found == 0) {
        cout << tmp << " code is not listed\n";
    } else {
        cout << "The price for product " << code << " is " << prc << "\n";
    }
    fstr.close();
    return 0;
}
```

### C.24.3 Suppose that each line of the students.txt file contains the names of the students and grades in two lessons, as follows:

| John | Morne | 7 | 8.12 |
| Sahil | Nehrud | 4.5 | 9 |
| Koon | Lee | 2 | 5.75 |

Write a program that reads each line of students.txt and stores in suc.txt the names and grades of the students with average grade greater than or equal to 5, while in fail.txt the students with average grade less than 5. The program should display the number of students written in file.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
    string fnm, lnm;
    int suc_stud, fail_stud;
    double grd1, grd2;

    ifstream fin("students.txt");
    if(fin.is_open() == false) {
        cout << "Error: students.txt can't be loaded\n";
        exit(EXIT_FAILURE);
    }
    ofstream fout_suc("suc.txt");
    if(fout_suc.is_open() == false) {
        fin.close();
        cout << "Error: suc.txt can't be created\n";
        exit(EXIT_FAILURE);
    }
    ofstream fout_fail("fail.txt");
    if(fout_fail.is_open() == false) {
        fin.close();
        fout_suc.close();
        cout << "Error: fail.txt can't be created\n";
        exit(EXIT_FAILURE);
    }
    suc_stud = fail_stud = 0;
    while(1) {
        fin >> fnm >> lnm >> grd1 >> grd2;
        if(!fin) {
            break;
        }
        if((grd1+grd2)/2 >= 5) {
            fout_suc << fnm << ' ' << lnm << ' ' << grd1 << ' ' << grd2 << '\n';
            suc_stud++;
        } else {
            fout_fail << fnm << ' ' << lnm << ' ' << grd1 << ' ' << grd2 << '\n';
            fail_stud++;
        }
    }
    cout << "Success: " << suc_stud << " Fail: " << fail_stud << endl;
    fin.close();
    fout_suc.close();
    fout_fail.close();
    return 0;
}
```

### C24.4 Write a program that reads the name of two files, compares them by line, and displays their common line. If the files have no common line, the program should display a message.

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
    bool found;
    string fname, str1, str2;

    cout << "Enter first file: ";
    cin >> fname;
    ifstream fin_f(fname.c_str());
    if(fin_f.is_open() == false) {
        cout << "Error: first file can't be loaded\n";
        exit(EXIT_FAILURE);
    }

    cout << "Enter second file: ";
    cin >> fname;
    ifstream fin_s(fname.c_str());
    if(fin_s.is_open() == false) {
        fin_f.close();
        cout << "Error: second file can't be loaded\n";
        exit(EXIT_FAILURE);
    }

    found = 0;
    while(1) {
        if(!getline(fin_f, str1) || !getline(fin_s, str2)) {
            break;
        }
        if(str1 == str2) {
            found = 1;
            break; /* Since the common line is found we can terminate the loop. */
        }
    }

    if(found == 0) {
        cout << "No common line\n";
    } else {
        cout << "Common line found: " << str1 << endl;
    }

    fin_f.close();
    fin_s.close();
    return 0;
}
```

### C24.5 A simple way to encrypt data by XOR them with a secret key. Write a program that reads a key character and the name of a file and encrypts it by XORing each character with the key. The encrypted characters should be stored in a second file selected by the user.

```cpp
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
    if(fin.is_open() == false) {
        cout << "Error: Input file can't be loaded\n";
        exit(EXIT_FAILURE);
    }

    cout << "Enter output file: ";
    cin >> fname;
    ofstream fout(fname.c_str());
    if(fout.is_open() == false) {
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

### C24.7 Define the class Country with private members: name, capital, and population. Suppose each line of the country.txt file contains the data of the respective country in the form:

name capital population
