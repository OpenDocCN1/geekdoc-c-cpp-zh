```
if (r !=t.res) {
    cout << "failure: test " << t.label
    << " binary_search: "
    << t.seq.size() << " elements, val==" << t.val
    << " -> " << t.res << '\n';
    ++error_count;
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
1.1 {1 2 3 5 8 13 21} 1}  
1.2 5{1 2 3 5 8 13 21} 1}  
1.3 8{1 2 3 5 8 13 21} 1}  
1.4 21{1 2 3 5 8 13 21} 1}  
1.5−7{1 2 3 5 8 13 21} 0}  
1.6 4{1 2 3 5 8 13 21} 0}  
1.7 22{1 2 3 5 8 13 21} 0}  
{2 1} 0}  
{3.1 {1} 1}  
{3.2 0{1} 0}  
{3.3 2{1} 0}
```

Here we see why we used a string label rather than a number: that way we can “number” our tests using a more flexible system – here using a decimal system to indicate separate tests for the same sequence. A more sophisticated format would eliminate the need to repeat a sequence in our test data file.

# ## 26.3.2.3 Random sequences

When we choose values to be used in testing, we try to outwit the implementers (who are often ourselves) and to use values that focus on areas where we know bugs can hide (e.g., complicated sequences of conditions, the ends of sequences,