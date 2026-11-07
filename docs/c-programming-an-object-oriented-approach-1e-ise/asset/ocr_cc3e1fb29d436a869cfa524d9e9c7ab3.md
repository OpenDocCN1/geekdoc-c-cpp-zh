# **Program 19.2** Showing the random-access nature of iterators (Continued)

```
```cpp
vector <int>::iterator iter1;
vector <int>::reverse_iterator iter2;
// Filling the vector with 10 elements
for (int i = 0; i < 10; i++)
{
    vec.push_back(i * 10);
}
// Using the regular iterator to print 40 followed by 20
cout << "Printing 40 followed by 20" << endl;
iter1 = vec.begin();
iter1 += 4;
cout << *iter1 << " ";
iter1 -= 2;
cout << *iter1 << endl;
// Using the reverse iterator to print 70 followed by 50
cout << "Printing 50 followed by 70" << endl;
iter2 = vec.rbegin();
iter2 += 4;
cout << *iter2 << " ";
iter2 -= 2;
cout << *iter2 << endl;
return 0;
}
```
```

```
```text
Run:
Printing 40 followed by 20
40  20
Printing 50 followed by 70
50  70
```
```

Figure 19.7 shows how the regular and reverse iterators can move backward and forward randomly.

**Insertion** The vector class defines several member functions that insert one or more items into the container. The insertion at the back is very efficient and does not require relocation of the items in the vector. Insertion in the middle and at the front require reallocation of items

![](bbox=[0.256, 0.794, 0.823, 0.901])

**Figure 19.7** Movement of regular and reverse iterators in a vector