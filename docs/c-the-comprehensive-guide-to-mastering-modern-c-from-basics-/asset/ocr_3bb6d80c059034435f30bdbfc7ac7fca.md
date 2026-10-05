```
void sortDataCont(vector<int> &data) { // entire container
    // exemplary -
    sort(data.begin(), data.end());
}
void sortDataIt(vector<int>::iterator b, 
    vector<int>::iterator e) { // unnecessarily specific
    // exemplary -
    sort(b, e);
}
```

Instead, define the functions as templates:

```
void sortDataCont(auto &data) {
    // exemplary
    sort(data.begin(), data.end());}
}
template<typename It>
void sortDataIt(It b, It e) {
    // exemplary
    sort(b, e);
}
```

Here I used data to pass the entire abbreviated function template using auto. Here the function performs a sort that works on various containers.

Don't forget that you (still) need to carefully consider whether the templated parameters of the functions need to be references &, pointers *, or consts. Iterators are usually passed by value.

However, you can be even more flexible if you define your function for ranges:

```
// https://godbolt.org/z/Y8KK3nEG3
void sortData(std::ranges::random_access_range auto &&data) {
```