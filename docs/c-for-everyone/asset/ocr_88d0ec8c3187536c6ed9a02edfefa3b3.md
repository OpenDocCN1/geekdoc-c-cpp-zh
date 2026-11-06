```
```cpp
void print_triangle(int side_length)
{
    if (side_length < 1) return;
    print_triangle(side_length - 1);
    for (int i = 0; i < side_length; i++)
    {
        cout << "[]";
    }
    cout << endl;
}

int main()
{
    cout << "Enter the side length: ";
    int input;
    cin >> input;
    print_triangle(input);
    return 0;
}
```
```

# Program Run

```
```text
Enter the side length: 10
[]
[][]
[][][]
[][][][]
[][][][][]
[][][][][][]
[][][][][][][]
[][][][][][][][]
[][][][][][][][][]
[][][][][][][][][][]
```
```

Recursion is not really necessary to print triangle shapes. You can use nested loops, like this:

```
```cpp
for (int i = 0; i < side_length; i++)
{
    for (int j = 0; j < i; j++)
    {
        cout << "[]";
    }
    cout << endl;
}
```
```

However, this pair of loops is a bit tricky. Many people find the recursive solution simpler to understand.

![](bbox=[0.113, 0.789, 0.198, 0.875])

# SELF CHECK

**38.** Consider this slight modification of the `print_triangle` function:

```
```cpp
void print_triangle(int side_length)
{
    if (side_length < 1) { return; }
    for (int i = 0; i < side_length; i++)
    {
        cout << "[]";
```
```