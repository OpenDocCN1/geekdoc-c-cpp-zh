
the point where we split it becomes the end of a subsequence, and we know that errors are likely near ends of sequences.

In general, we look for:

- Extreme cases (large, small, strange distributions of input, etc.)
- Boundary conditions (anything near a limit)

What that really means, depends on the particular program we are testing.

## 26.3.2.2 A simple test harness

We have two categories of tests: tests that should succeed (e.g., searching for a value that’s in a sequence) and tests that should fail (e.g., searching for a value in an empty sequence). For each of our sequences, let’s construct some succeeding and some failing tests. We will start from the simplest and most obvious and proceed to improve until we have something that’s good enough for our *binary_search* example:

```cpp
vector<int> v { 1,2,3,5,8,13,21 };
if (binary_search(v.begin(),v.end(),1) == false) cout << "failed";
if (binary_search(v.begin(),v.end(),5) == false) cout << "failed";
if (binary_search(v.begin(),v.end(),8) == false) cout << "failed";
if (binary_search(v.begin(),v.end(),21) == false) cout << "failed";
if (binary_search(v.begin(),v.end(),-7) == true) cout << "failed";
if (binary_search(v.begin(),v.end(),4) == true) cout << "failed";
if (binary_search(v.begin(),v.end(),22) == true) cout << "failed";
```

This is repetitive and tedious, but it will do for a start. In fact, many simple tests are nothing but a long list of calls like this. This naïve approach has the virtue of being extremely simple. Even the newest member of the test team can add a new test to the set. However, we can usually do much better. For example, when something failed here, we are not told which test failed. That’s unacceptable. Also, writing tests is no excuse for regressing to “cut and paste” programming. We need to consider the design of our testing code, just like any other code. So:

```cpp
vector<int> v { 1,2,3,5,8,13,21 };
for (int x : {1,5,8,21,-7,2,44})
    if (binary_search(v.begin(),v.end(),x) == false) cout << x << " failed";
```

Assuming that we will eventually have dozens of tests, this will make a huge difference. For testing real-world systems, we often have many thousands of tests, so being precise about what test failed is essential.

Before going further, note another example of (semi-systematic) testing technique: we tested with correct values, choosing some from the ends of the sequence and some from “the middle.” For this sequence we could have tried all values, but typically that’s not a realistic option. For the failing values, we chose one from each end and one in the middle. Again, this is not perfectly systematic, but we begin to see a pattern that is useful whenever we deal with sequences of values or ranges of values – and that’s very common.

What’s wrong with these tests?

- We (initially) wrote the same things repeatedly.
- We (initially) numbered the tests manually.
- The output is very minimal (not very helpful).

After looking at this for a while, we decided to keep our tests as data in a file. Each test would contain an identifying label, a value to be looked up, a sequence, and an expected result. For example:

`{ 27 7 { 1 2 3 5 8 13 21} 0}`

This is test number **27**. It looks for **7** in the sequence `{1, 2, 3, 5, 8, 13, 21}` expecting the result **0** (meaning **false**). Why do we put the test inputs in a file rather than placing them right into the text of the test program? Well, in this case we could have typed the tests straight into the program text, but having a lot of data in a source code file can be messy, and often, we use programs to generate test cases. Machine-generated test cases are typically in data files. Also, we can now write a test program that we can run with a variety of files of test cases:

```cpp
struct Test {
    string label;
    int val;
    vector<int> seq;
    bool res;
};

istream& operator>>(istream& is, Test& t);  // use the described format

int test_all(istream& is)
{
    int error_count = 0;
    for (Test t; is>>t; ) {
        bool r = binary_search(t.seq.begin(), t.seq.end(), t.val);
        if (r != t.res) {
            cout << "failure: test " << t.label
            << " binary_search: "
            << t.seq.size() << " elements, val==" << t.val
            << " -> " << t.res << '\n';
            ++error_count;
        }
    }
    return error_count;
}
int main()
{
    int errors = test_all(ifstream("my_tests.txt"));
    cout << "number of errors: " << errors << "\n";
}
```

Here is some test input using the sequences we listed above:

```
{1.1 1 {1 2 3 5 8 13 21} 1}
{1.2 5 {1 2 3 5 8 13 21} 1}
{1.3 8 {1 2 3 5 8 13 21} 1}
{1.4 21 {1 2 3 5 8 13 21} 1}
{1.5 -7 {1 2 3 5 8 13 21} 0}
{1.6 4 {1 2 3 5 8 13 21} 0}
{1.7 22 {1 2 3 5 8 13 21} 0}
{2.1 1 {2} 0}
{3.1 1 {1} 1}
{3.2 0 {1} 0}
{3.3 2 {1} 0}
```

Here we see why we used a string label rather than a number: that way we can “number” our tests using a more flexible system – here using a decimal system to indicate separate tests for the same sequence. A more sophisticated format would eliminate the need to repeat a sequence in our test data file.

## 26.3.2.3 Random sequences

When we choose values to be used in testing, we try to outwit the implementers (who are often ourselves) and to use values that focus on areas where we know bugs can hide (e.g., complicated sequences of conditions, the ends of sequences, loops, etc.). However, that’s also what we did when we tried to write and debug the code. So, we might repeat a logical mistake from the design when we design the tests and completely miss a problem. This is one reason it is a good idea to have someone different from the developer(s) involved with designing the tests. We have one technique that occasionally helps with that problem: just generate (a lot of) random values. For example, here is a function that writes a test description to `cout` using `randint()` from §24.7 and `std_lib_facilities.h`:

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

Note that we did not use `binary_search` to see if the random `val` was in the random sequence. We can’t use what we are testing to determine the correct value of a test. Actually, `binary_search` isn’t a particularly suitable example of the brute-force random number approach to testing. We doubt that this will find any bugs that are not picked up by our “hand-crafted” tests, but often this technique is useful. Anyway, let’s make a few random tests:

```cpp
int no_of_tests = randint(100);    // make about 50 tests
for (int i = 0; i<no_of_tests; ++i) {
    string lab ="rand_test_";
    make_test(lab+to_string(i), // to_string from §23.2
    randint(500), // number of elements
    0, // base
    randint(50)); // spread
}
```

Generated tests based on random numbers are particularly useful when we need to test the cumulative effects of many operations where the result of an operation depends on how earlier operations were handled, that is, when a system has state; see §5.2.

The reason that random numbers are not all that useful for **binary_search** is that each search of a sequence is independent of all other searches of that sequence. That of course assumes that the implementation of **binary_search** hasn't done something terminally stupid, such as modifying its sequence. We have a better test for that (exercise 5).

## 26.3.3 Algorithms and non-algorithms

We have used **binary_search()** as an example. It’s a proper algorithm with:

- Well-specified requirements on its inputs
- A well-specified effect on its inputs (in this case, no effects)
- No dependencies on objects that are not its explicit inputs
- Without serious constraints imposed by the environment (e.g., no specified time, space, or resource-sharing requirements)

It has obvious and explicitly stated pre- and post-conditions (§5.10). In other words, it’s a tester’s dream. Often, we are not so lucky: we have to test messy code that (at best) is defined by a somewhat sloppy English text and a couple of diagrams.

Wait a minute! Are we indulging in sloppy logic here? How can we talk about correctness and testing when we don't have a precise specification of what the code is supposed to do? The problem is that much of what needs to be done in software is not easy to specify in perfectly clear mathematical terms. Also, in many cases where it in theory could be specified like that, the math is beyond the abilities of the programmers who write and test the code. So we are left with the ideal of perfectly precise specifications and a reality of what someone (such as us) can manage under real-world conditions and time pressures.

So, assume that you have a messy function that you have to test. By “messy” we mean:

- **Inputs:** Its requirements on its (explicit or implicit) inputs are not specified quite as well as we would like.
- **Outputs:** Its (explicit or implicit) outputs are not specified quite as well as we would like.
- **Resources:** Its use of resources (time, memory, files, etc.) is not specified quite as well as we would like.
