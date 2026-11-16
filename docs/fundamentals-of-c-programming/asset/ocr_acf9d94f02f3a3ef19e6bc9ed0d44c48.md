```
* locate(a, seek)
*
* Returns the index of element seek in vector a.
* Returns -1 if seek is not an element of a.
*
* a is the vector to search.
* seek is the element to find.
*/
int locate(const std::vector<int>& a, int seek) {
    int n = a.size();
    for (int i = 0; i < n; i++)
        if (a[i] == seek)
            return i; // Return position immediately
    return -1; // Element not found
}
```

```
/*
 * format(i)
 *
 * Prints integer i right justified in a 4-space
 * field. Prints "****" if i > 9,999.
 */
void format(int i) {
    if (i > 9999)
        std::cout << "****" << '\n'; // Too big!
    else
        std::cout << std::setw(4) << i;
}
```

```
/*
 * print(v)
 *
 * Prints the contents of an int vector.
 * v is the vector to print.
 */
void print(const std::vector<int>& v) {
    for (int i = 0; i < v.size(); i++)
        format(i);
}
```

```
/*
 * display(a, value)
 *
 * Draws an ASCII art arrow showing where
 * the given value is within the vector.
 * a is the vector.
 * value is the element to locate.
 */
void display(const std::vector<int>& a, int value) {
    int position = locate(a, value);
    if (position >= 0) {
        print(a);
        std::cout << '\n';
        position = 4*position + 7; // Compute spacing for arrow
        std::cout << std::setw(position);
        std::cout << " ^\n";
        std::cout << std::setw(position);
        std::cout << " | " << '\n';
        std::cout << " | " << '\n';
    }
}
```