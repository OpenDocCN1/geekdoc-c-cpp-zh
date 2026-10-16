and places a copy of each unique vector element on a list:

```
bool operator<(const Entry& x, const Entry& y) // less than
{
return x.name<y.name; // order Entrys bytheir names
}
```

```
void f(vector<Entry>& vec, list<Entry>& lst) {
sort(vec.begin(),vec.end()); // use < for order
unique_copy(vec.begin(),vec.end(),lst.begin()); // don’t copyadjacent equal elements
}
```

The standard algorithms are described in Chapter 32. They are expressed in terms of sequences of elements. A sequence is represented by a pair of iterators specifying the first element and the onebeyond-the-last element:

# Section 4.5 Algorithms 103

iterators: begin() end()

elements:

In the example, sort() sorts the sequence defined by the pair of iterators vec.begin() and vec.end() – which just happens to be all the elements of a vector. For writing (output), you need only to specify the first element to be written. If more than one element is written, the elements following that initial element will be overwritten. Thus, to avoid errors, lst must have at least as many elements as there are unique values in vec.

If we wanted to place the unique elements in a new container, we could have written:

```
list<Entry> f(vector<Entry>& vec)
{
list<Entry> res;
sort(vec.begin(),vec.end());
unique_copy(vec.begin(),vec.end(),back_inser ter(res)); // append to res
return res;
}
```

A back_inser ter() adds elements at the end of a container, extending the container to make room for them (§33.2.2). Thus, the standard containers plus back_inser ter()s eliminate the need to use errorprone, explicit C-style memory management using realloc() (§31.5.1). The standard-library list has a move constructor (§3.3.2, §17.5.2) that makes returning res by value efficient (even for listsof thousands of elements).

If you find the pair-of-iterators style of code, such as sort(vec.begin(),vec.end()), tedious, you can define container versions of the algorithms and write sort(vec) (§4.5.6).

# 4.5.1 Use of Iterators

When you first encounter a container, a few iterators referring to useful elements can be obtained; begin() and end() are the best examples of this. In addition, many algorithms return iterators. For example, the standard algorithm find looks for a value in a sequence and returns an iterator to the element found: