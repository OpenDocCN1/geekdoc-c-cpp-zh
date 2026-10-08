```
```cpp
cout << "Jill's high " << *jill_high << "; Jack's high " << *jack_high;
// ...
delete[] jack_data;
delete jill_data;
}
```

```

For the two calls here, the **Iterator** template argument type for `high()` is **double\*.** Apart from (finally) getting the code for `high()` correct, there is apparently no difference from our previous solution. To be precise, there is no difference in the code that is executed, but there is a most important difference in the generality of our code. The templated version of `high()` can be used for every kind of sequence that can be described by a pair of iterators. Before looking at the detailed conventions of the STL and the useful standard algorithms that it provides to save us from writing common tricky code, let's consider a couple of more ways of storing collections of data elements.

# **TRY THIS**

We again left a serious error in that program. Find it, fix it, and suggest a general remedy for that kind of problem.

# ## 20.4 Linked lists

Consider again the graphical representation of the notion of a sequence:

![](bbox=[0.23, 0.62, 0.66, 0.7])

Compare it to the way we visualize a **vector** in memory:

![](bbox=[0.24, 0.74, 0.65, 0.83])

Basically, the subscript **0** identifies the same element as does the iterator **v.begin()**, and the subscript **v.size()** identifies the one-beyond-the-last element also identified by the iterator **v.end()**.