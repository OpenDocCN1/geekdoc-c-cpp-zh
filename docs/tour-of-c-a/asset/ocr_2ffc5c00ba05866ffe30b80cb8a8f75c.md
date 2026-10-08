```
return res;
}
```

This is obviously one of many ways to compute the sum of a sequence of numbers.
Consider what makes this code less general than it needs to be:

+   - Why just ints?
- Why just vectors?
- Why accumulate in a double?
- Why start at 0?
- Why add?

Answering the first question by making the concrete types into template arguments, we have the simplest form of the standard-library accumulate algorithm:

Click here to view code image

```
template<forward_iterator Iter, Arithmetic<iter_value<Iter>> Val>
Val accumulate(Iter first, Iter last, Val res)
{
  for (auto p = first; p!=last; ++p)
    res += p;
  return res;
}
```

Here, we have:

+   - The data structure to be traversed has been abstracted into a pair of iterators representing a sequence ($8.2.4, $13.1).
- The type of the accumulator has been made into a parameter.
- The type of the accumulator must work with the iterator's value type (the element type of sequence).
- The initial value is an input; the type of the accumulator is the type of this initial value.

A quick examination — even better — measurement will show that the code generated for calls with a variety of data structures is identical to what you get from hand-coded examples.
Consider:

Click here to view code image

```
void use(const vector<int>& vec, const list<double>& lst)
{
  auto sum = accumulate(begin(vec),end(vec),0.0); // accumulate in double
  auto sum2 = accumulate(begin(lst),end(lst),sum);
  // ...
}
```

The process of generalizing from a concrete piece of code (and preferably from several) while preserving performance is called lifting. Conversely, the best way to develop a template is often to

+   - first, write a concrete version
- then, debug, test, and measure