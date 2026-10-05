# 17.6. FINE TUNING INHERITANCE

```
for (int j = i + 1; j < n; j++)
    if (compare.compare(a[j], a[small]))
        small = j; // Found a smaller value
// Swap a[i] and a[small], if a smaller value was found
    if (i != small)
        compare.swap(a[i], a[small]);
```

```
/*
 * Print the contents of an integer vector
 * a is the vector to print.
 * a is not modified.
 */
```

```
void print(const vector<int>& a) {
    int n = a.size();
    cout << '<';
    if (n > 0) {
        cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            cout << ', ' << a[i];
    }
    cout << '>';n
```

```
/*
 * less_than(a, b)
 * Returns true if a < b; otherwise, returns
 * false.
 */
```

```
bool less_than(int a, int b) {
    return a < b;
}
```

```
/*
 * greater_than(a, b)
 * Returns true if a > b; otherwise, returns
 * false.
 */
```

```
bool greater_than(int a, int b) {
    return a > b;
}
```

```
int main() {
    // Make a vector of integers
    vector<int> original { 23, -3, 4, 215, 0, -3, 22, 100, 88, -10 };

    // Make a copy of the original vector
    vector<int> working = original;
    cout << "Before: ";
    print(working);
    cout << endl;
    Comparer lt(less_than), gt(greater_than);
    selection_sort(working, lt);
```