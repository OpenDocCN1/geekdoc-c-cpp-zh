# 12.3. SEARCH

```
int first = 0,               // Initially the first position
last = a.size() - 1,     // Initially the last position
mid: {\                    // The middle of the vector
while (first < last) {
    mid = first + (last - first + 1)/2;
    if (a[mid] == seek)
        return mid;               // Found it
    } else if (a[mid] > seek)
        last = mid - 1;           // continue with 1st half
    else                      // a[mid] < seek
        first = mid + 1;         // continue with 2nd half
}
return -1;                   // Not there
```

```
/*
* Prints integer i right justified in a 4-space
* field. """" if i > 9999.
/
```

```
void print(int i) {
    if (i > 9999)
        cout << """" << endl;   // Too big!
    else
        cout << setw(4) << i;
}
```

```
/*
* print(v)
* Prints the contents of an int vector.
* v is the vector to print.
/
```

```
void print(const vector<int>& v) {
    for (int i : v)
        format(i);
}
```

```
/*
* display(a, value)
* Draws an ASCII arrow showing where
* the given value is within the vector.
* a is the element to locate.
* value is the element.
/
```

```
void display(const vector<int>& a, int value) {
    int position = binary_search(a, value);
    if (position >= 0) {
        print(a);                   // Print contents of the vector
        cout << endl;
        position = 4*position + 7;     // Compute spacing for arrow
        cout << setw(position);
        cout << "";
        cout << setw(position) << endl;
    }
```