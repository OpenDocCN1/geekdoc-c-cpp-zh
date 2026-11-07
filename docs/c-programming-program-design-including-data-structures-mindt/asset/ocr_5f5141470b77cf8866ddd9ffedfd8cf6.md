```
```cpp
copy (vecList.rbegin() + 3, vecList.rend() - 1,
     vecList.rbegin());
copy (vecList.begin(), vecList.end(), screen);
cout << endl;
```
```

8. What is the output of the following C++ code? (7, 8)

```
```cpp
list<int> intList;
int i;

for (i = 0; i < 5; i++)
    intList.push_back(i * (i + 1));

for (auto p : intList)
    cout << p << " ";
cout << endl;
```
```

9. What is the output of the following C++ code? (7, 8)

```
```cpp
list<int> intList(5);

int x = 0;

for (auto &p : intList)
{
    if (x % 2 == 0)
        p = x * (x + 2);
    else
        p = (x - 1) * (x + 3);
    x++;
}

for (auto p : intList)
    cout << p << " ";
cout << endl;
```
```

10. What is the output of the following program segment? (8)

```
```cpp
list <int> intList = {27, 3, 3, 3, 45, 45, 12, 3,
                      3, 1, 1, 1};
ostream_iterator<int> screen(cout, " ");

copy(intList.begin(), intList.end(), screen);
cout << endl;

intList.unique();

copy(intList.begin(), intList.end(), screen);
cout << endl;
```
```

11. Suppose that intList1, intList2, and intList3 are list containers and (8)

+   - `intList1 = {13, 15, 16, 18, 90, 30, 11, 88, 26}`
+   - `intList2 = {7, 8, 19, 90, 15}`
+   - `intList3 = {12, 12, 14, 20, 20, 13, 13, 13}`