
On the other hand, when the address of the structure is passed, the function may change the values of its members. For example, let's change test(), in order to modify the members of st:

```
void test(Student *ptr);

int main() {
  ...
  test(&st);
  std::cout << st.name << ' ' << st.code << ' ' << st.grd << '\n';
}
```

```
void test(Student *ptr) {
  ptr->name = "new";
  ptr->code = 30;
  ptr->grd = 7;
}
```

When test() is called, we have ptr = &st. Therefore, since ptr points to the address of st, the function may change the values of its members. As a result, the program displays: new 30 7

When a structure is passed to a function, its members are copied to the members of the respective parameter. Note that if the structure is large or the function is called many times, this copy operation may increase memory requirements and add a time overhead. On the other hand, when the address of the structure is passed through a pointer or reference, the members are not copied.

> For better performance, pass the address of the structure, not the structure itself, even if the function won't change the values of its members.

To prevent the function from changing the values of the members, we declare the pointer or the reference as const. For example:

```
void test(const Student *ptr);
```

now, test() cannot modify the members of the structure pointed to by ptr.

# EXERCISES

C.13.1 What is the output of the following program?

```
#include <iostream>

struct Student {
  char name[50];
  int code;
  float grd;
};
```

Student *test(), st;

```
int main()
{
    Student stud = {"somebody", 1111, 7.5}, *ptr = &stud;

    *ptr = *test();
    std::cout << ' ' << ptr->name << ' ' << ptr->code << ' ' << ptr->grd << ' '\n';
    return 0;
}
```

```
Student *test()
{
    return &st;
}
```

**Answer:** Since test() returns the address of st, *test() is equivalent to st. Since ptr points to the address of stud, *ptr is equivalent to stud. Therefore, the expression *ptr = *test(); is equivalent to stud = st; Since the global variable is initialized with zero, the program outputs: 0 0.

**C.13.2** Define the structure City with members: name, country name, and population. Write a program that uses this type to read the data of 100 cities and store them in an array. The program should read the name of a country and a number and display the cities whose population is greater than the input number. To read the data of each city write a loop which uses the following variables:

```
int main()
{
    City *ptr, cities[SIZE];
    ...
}
```

**Answer:**

```
#include <iostream>
#include <string>
using std::cout;
using std::cin;
using std::string;

const int SIZE = 100;

struct City
{
    string name;
    string cntr;
    int pop;
}
```

```cpp
int main()
{
    bool found;
    int i, pop;
    string cntr;
    City *ptr, cities[SIZE];

    for(ptr = cities; ptr < cities+SIZE; ptr++) { /* When ptr increases to the next element of the array, that is, to the next structure. */
    {
        cout << "\nCity: ";
        getline(cin, ptr->name);

        cout << "Country: ";
        cin >> ptr->cntr;

        cout << "Population: ";
        cin >> ptr->pop;
        cin.get();
    }
    cout << "\ncountry to search: ";
    getline(cin, cntr);

    found = 0; for(i = 0; i < SIZE; i++) {
        if((cities[i].cntr == cntr) && (cities[i].pop > pop)) {
            found = 1;
            cout << cities[i].name << ' ' << cities[i].pop << '\n';
        }
    }
    if(found == 0)
        cout << "\nNo city found\n";
    return 0;
}
```

**C.13.3** Define the structure Time with members: hours, minutes, and seconds. Write a function that takes as parameter a pointer to an integer and converts that to hours, minutes, and seconds. These values should be stored into the members of the structure of Time. Write a program that reads a number of seconds, calls the function, and displays the members of the returned structure.

```
#include <iostream>

struct Time {
    int hours;
    int mins;
    int secs;
};

Time mk_time(const int *ptr);

int main() {
    int secs;
    Time t;

    std::cout << "Enter seconds: ";
    cin >> secs;

    t = mk_time(&secs);
    std::cout << "\NH:" << t.hours << " M:" << t.mins << " S:" << t.secs << '\n';

    return 0;
}
```

```
Time mk_time(const int *ptr)
{
    Time tmp;

    tmp.hours = *ptr/3600;
    tmp.mins = (*ptr%3600)/60;
    tmp.secs = *ptr%60;
    return tmp;
}
```

**Comments:** To avoid copying the structure returned from mk_time() we could pass the address of structure. For example, we could change the return type to void and pass the address of t to mk_time(). Thus, the function modifies the structure of the calling function instead of returning a new structure.

```
void mk_time(const int *ptr, Time *tmp)
{
    tmp->hours = *ptr/3600;
    tmp->mins = (*ptr%3600)/60;
    tmp->secs = *ptr%60;
}
```

**C.13.4** Define the structure Book with members: Write a void function that takes as pointers to structures of type Book and returns the structure with the higher code. Check the case of the same codes and print a related message. Write a program that reads and stores the data of books into an array of structures. Then, the program should read two numbers in [1, 10] that represent structure indexes in the array. The program should check the validity of the input numbers and use the function to display the data of the structure with the higher code.

```
#include <iostream>
#include <string>
using std::cout;
using std::cin;

struct Book
{
    std::string title;
    int code;
    float prc;
};

void max_code(const Book *b1, const Book *b2, Book *fin);

int main()
{
    const int SIZE = 10;
    int i, j;
    Book fin, b[SIZE];

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
        cout << "\nEnter two numbers [1-" << SIZE << ": ";
        cin >> i >> j;
    } while ((i == j) || i > SIZE || j >= SIZE || i < 1 || j < 1);

    i--;
    j--;
    max_code(&b[i], &b[j], &fin);
    if(fin.code != -1)
        cout << "\nNN: " << fin.title << " C:" << fin.code << " P:" << fin.prc << "\n";
    else
        cout << "\nBooks have the same code: " << b[i].code << "\n";
    return 0;
}
```

```
void max_code(const Book *b1, const Book *b2, Book *fin)
{
    if (b1->code > b2->code)
        *fin = *b1;
    else if (b1->code < b2->code)
        *fin = *b2;
    else
        fin->code = -1;
}
```

**C.13.5** Define the structure Product with members: name, code, and price. Write a function that takes as parameters a vector of such structures and the code of a product. The function should check if a product in the vector has the same code and, if so, return a pointer to the respective structure, otherwise nullptr. Write a program that uses the type Product to read the data of products and store them in a vector. If the user enters a negative value for price, the insertion of data should terminate. Then, the program should use the function to display the product's name and price, if found.

```
#include <iostream>
#include <string>
#include <vector>
using namespace std;

struct Product
{
  string name;
  int code;
  float prc;
};
```

```
const Product *find_prod(const vector<Product>& v, int code);
```

```cpp
int main() {
  const Product *ptr;
  int code;
  float prc;
  Product tmp;
  vector<Product> prod;
  while (1) {
    cout << "\nPrice: ";
    cin >> prc;
    if (prc <= 0) {
      break;
    }
    tmp.prc = prc;
    cin.get();
    cout << " <<Name: ";
    getline(cin, tmp.name);
    cout << " <<Code: ";
    cin >> tmp.code;
    prod.push_back(tmp);
  }
  if (prod.size() == 0) {
    cout << "\nNo product is stored\n";
    return 0;
  }
  cout << "\nEnter code to search: ";
  cin >> code;
  ptr = find_prod(prod, code);
  if (ptr == nullptr) {
    cout << "\nNo product with code = " << code << " '\n";
  } else {
    cout << "\nNN: " << ptr->name << " C:" << code << " P:" << ptr->prc << "\n";
  }
  return 0;
}
```

```cpp
const Product *find_prod(const vector<Product>& v, int code) {
  for (int i = 0; i < v.size(); i++) {
    if (v[i].code == code) {
      return &v[i];
    }
  }
  return nullptr;
}
```
