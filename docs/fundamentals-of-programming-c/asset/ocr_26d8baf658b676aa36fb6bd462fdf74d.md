# 12.5. RANDOMLY PERMUTING A VECTOR

```
}
cout << "";
}
```

> /*
* Returns a pseudorandom number in the range begin..end - 1,
* Returns 0 if begin >= end.
*/

```
int random(int begin, int end) {
    if (Begin >= end)
        return 0;
    else {
        int range = end - begin;
        return begin + rand()%range;
    }
}
```

> /*
* Randomly permute a vector of integers.
* a is the vector to permute, and n is its length.
*/

```
void permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // Select a pseudorandom location from the current
        // location to the end of the collection
        swap(a[i], a[random(i, n)]);
    }
}
```

> /* Randomly permute a vector? */

```
void faulty_permute(vector<int>& a) {
    int n = a.size();
    for (int i = 0; i < n; i++) {
        // Select a pseudorandom position somewhere in the collection
        swap(a[i], a[random(0, n)]);
    }
}
```

> /* Classify a vector as one of the six permutations */

```
int classify(const vector<int>& a) {
    switch (100*a[0] + 10*a[1] + a[2]) {
        case 123: return 0;
        case 132: return 1;
        case 213: return 2;
        case 231: return 3;
        case 312: return 4;
        case 321: return 5;
    }
    return -1;
}
```

> /* Report the accumulated statistics */

```
void report(const vector<int>& a) {
    cout << "1,2,3: " << a[0] << endl;
}
```