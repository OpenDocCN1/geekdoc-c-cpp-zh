}
ll... use r.ptr ...
}

We could argue that encoding failure as the end iterator or a nullptr is more elegant, but that can express just one kind of failure. Consequently, we would like to return two separate values. Defining a specific named struct for each pair of values works well and is quite readable if the names of the "pair of values" structs and their members are well chosen. However, for large code bases it can lead to a proliferation of names and conventions, and it doesn't work for generic code where consistent naming is essential. The standard library provides pair as a general support for the "pair of values" cases. Using pair, our simple example becomes:

Click here to view code image

```
pair<Entry,Error_code>complex_search(vector<Entry>&, const string& s)
{
    Entry found = nullptr;
    Error_code err = Error_code::found;
    ll... search for s in v ...
    return (found,err);
}
```

```
void user(const string& s)
{
    auto r = complex_search(entry_table,s); // search entry_table
    if (r != Error_code::good) {
        ll... handle error ...
    }
    ll... use r.ptr ...
}
```

The members of pair are named first and second. That makes sense from an implementer's point of view, but in application code we may want to use our own names. Structured binding (§3.4.5) can be used to deal with:

Click here to view code image

```
void user(const string& s)
{
    auto [ptr,success] = complex_search(entry_table,s); // search entry_table
    if (success != Error_code::good) {
        ll... handle error ...
    }
    ll... use r.ptr ...
}
```

The standard-library pair from <utility> is frequently used for "pair of values" cases in the standard library. For example, the standard-library algorithm equal_range pair iterators signifying a subsequence meeting a predicate:

Click here to view code image

```
template<typename Forward_iterator, typename T, typename Compare = Compare<T>>
pair<Forward_iterator, Forward_iterator>
equal_range(Forward_iterator first, Forward_iterator last, const T& val, Compare& cmp = Compare());
```

Given a sorted sequence [first:last], equal_range() will return the pair representing the subsequence