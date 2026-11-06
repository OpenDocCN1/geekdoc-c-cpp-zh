# LISTING 6-12: *(continued)*

```
```cpp
ostream& operator << (ostream &out, const Duck &duck) {
    cout << "(" << duck.name;
    cout << ", " << duck.weight;
    cout << ", " << duck.length;
    cout << ")";
    return out;
}

void Dump(list<Duck> *mylist) {
    list<Duck>::iterator iter = mylist->begin();
    while (iter != mylist->end())
    {
        cout << *iter << endl;
        iter++;
    }
}

list<Duck>::iterator Move(list<Duck> *mylist, int pos) {
    list<Duck>::iterator res = mylist->begin();
    for (int loop = 1; loop <= pos; loop++)
    {
        res++;
    }
    return res;
}

bool operator < (const Duck& first, const Duck& second) {
    return first.name < second.name;
}

int main() {
    list<Duck> Inarow;

    // Push some at the beginning
    Duck d1 = {"Jim", 20, 15}; // Braces notation!
    Inarow.push_front(d1);
    Duck d2 = {"Sally", 15, 12};
    Inarow.push_front(d2);

    // Push some at the end
    Duck d3 = {"Betty", 18, 25};
    Inarow.push_front(d3);
    Duck d4 = {"Arnold", 19, 26};
    Inarow.push_front(d4);
```
```