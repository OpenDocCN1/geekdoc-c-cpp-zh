```
```cpp
int main()
{
    vector<int> vecList(8);
    ostream_iterator<int> screen(cout, " ");
    generate(vecList.begin(), vecList.end(), nextNum);
    cout << "Line 4: vecList after filling with "
         << "numbers: ";
    copy(vecList.begin(), vecList.end(), screen);
    cout << endl;
    generate_n(vecList.begin(), 3, nextNum);
    cout << "Line 8: vecList after filling the "
         << "first three elements " << endl
         << "         with the next number: ";
    copy(vecList.begin(), vecList.end(), screen);
    cout << endl;
    return 0;
}

int nextNum()
{
    static int n = 1;
    return n++;
}
```
```

# Sample Run:

```
```text
Line 4: vecList after filling with numbers: 1 2 3 4 5 6 7 8
Line 8: vecList after filling the first three elements
         with the next number: 9 10 11 4 5 6 7 8
```
```

This program contains a value-returning function, nextNum, which contains a static variable n initialized to 1. A call to this function returns the current value of n and then increments the value of n. Therefore, the first call of nextNum returns 1, the second call returns 2, and so on.

The statements in Lines 1 and 2 declare vecList to be a sequence container of size 8 and screen to be an ostream iterator initialized to cout with the delimit character space. The statement in Line 3 uses the function generate to fill vecList by successively calling the function nextNum. Notice that after the statement in Line 3 executes, the value of the static variable n of nextNum is 9. The statement in Line 5 outputs the elements of vecList. The statement in Line 7 calls the function generate_n to fill the first three elements of vecList by calling the function nextNum three times. The starting position is