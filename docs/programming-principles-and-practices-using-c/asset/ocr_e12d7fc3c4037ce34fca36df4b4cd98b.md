loops, etc.). However, that’s also what we did when we tried to write and debug the code. So, we might repeat a logical mistake from the design when we design the tests and completely miss a problem. This is one reason it is a good idea to have someone different from the developer(s) involved with designing the tests. We have one technique that occasionally helps with that problem: just generate (a lot of) random values. For example, here is a function that writes a test description to `cout` using `randint()` from §24.7 and `std_lib_facilities.h`:

```
```cpp
void make_test(const string& lab, int n, int base, int spread)
    // write a test description with the label lab to cout
    // generate a sequence of n elements starting at base
    // the average distance between elements is uniformly distributed
    // in [0:spread]
{
    cout << "{" << lab << " " << n << " { ";
    vector<int> v;
    int elem = base;
    for (int i = 0; i<n; ++i) {   // make elements
        elem+= randint(spread);
        v.push_back(elem);
    }
    int val = base+ randint(elem-base);     // make search value
    bool found = false;
    for (int i = 0; i<n; ++i) {     // print elements and see if val is found
        if (v[i]==val) found = true;
        cout << v[i] << " ";
    }
    cout << "}" << found << " }\n";
}
```
```

Note that we did not use `binary_search` to see if the random `val` was in the random sequence. We can’t use what we are testing to determine the correct value of a test. Actually, `binary_search` isn’t a particularly suitable example of the brute-force random number approach to testing. We doubt that this will find any bugs that are not picked up by our “hand-crafted” tests, but often this technique is useful. Anyway, let’s make a few random tests:

```
```cpp
int no_of_tests = randint(100);    // make about 50 tests
for (int i = 0; i<no_of_tests; ++i) {
    string lab ="rand_test_";
    make_test(lab+to_string(i), // to_string from §23.2
```
```