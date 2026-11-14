```
{
    using namespace std;
    vector <int> v;
    v.push_back(4);
    v.push_back(7); v.push_back(9);
    vector<int>::iterator it= find(v.begin(), v.end(), 4);
    cout << "After " << *it << " comes " << *(it+1) << '\n';
    v.insert(it+1, 5);    // insert value 5 at pos. 2
    v.erase(v.begin());   // delete entry at pos. 1
    cout << "Size = " << v.size() << ", capacity = "
        << v.capacity() << '\n';
    // The following block emulates shrink_to_fit() in C++11
    {
        vector<int> tmp(v);
        swap(v, tmp);
    }
    v.push_back(7);
    for(vector<int>::iterator it= v.begin(), end= v.end();
        it != end; ++it)
        cout << *it << ",";
    cout << '\n';
}
```

In contrast to C++11, we have to spell out all iterator types and deal with quite cumbersome initialization and shrinking. Only when backward compatibility is really important should we bother with this old-style coding.

# C++11 A.7.2 variant

=> c++17/variant_example_nerdy.cpp

To push the C++17 features more to their limits, we revise the variant example from Section 4.4.3 with overloaded lambdas. Instead of defining an overloaded functor for `visit` upfront we create it on the fly with a lambda for each overload:

Click here to view code image

```
for (const auto& mv : v)
  visit(overloaded{
    [&r](int i){r.ints++;r.symbs+= floor(log10(i)) +
    1;},
    [&r](double d){r.doubles++; r.symbs+= 15;},
```