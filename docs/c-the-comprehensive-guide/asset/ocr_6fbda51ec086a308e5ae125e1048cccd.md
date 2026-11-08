> > **Spans Are Different from Ranges**
> >
> > For contiguous containers like string and vector, simpler variants of views into containers are possible: string_view, the span that has existed since C++20, and the mdspan added with C++23. These should not be confused with ranges and their views. However, a span is also a borrowed_range and therefore compatible in many places.

# ## Combining Views and Pipelines with Ranges

But that's not all. With ranges, views were introduced, and with views, pipelines. Are you coming from Java? Do you like streams? Functional programming? Composition? Then you'll love views. Views are ranges that do not store elements themselves but access other ranges. So they are a kind of "perspective" on other ranges. And pipelines are a way to combine views. So they are something like a connection-cable for views.

With the pipe operator |, you create and combine views. We will get more specific about algorithms in a moment, but I want to briefly show you what a pipeline of views looks like in code. The next listing shows how this previously looked with algorithms.

```
```
// https://godbolt.org/z/ar7ee3TP
using namespace std;
vector in { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
vector<int> tmp();
vector<int> out();
copy_if(in.begin(), in.end(), back_inserter(tmp), [](int i) { return i%3 == 0;
});
transform(tmp.begin(), tmp.end(), back_inserter(out), [](int i) {return i*1;
});
```
```

**Listing 24.4** One algorithm after another with iterators.

And in the next one, you can see that it is significantly more elegant with a pipeline of views.

```
```
// https://godbolt.org/z/TGIqd31Mq
using namespace std; namespace views = std::ranges::views;
vector in { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
auto out = in
    | views::filter([](int i) { return i%3 == 0; })
    | views::transform([](int i) {return i*1;});
```
```

**Listing 24.5** A pipeline of views instead of algorithms.

With the first | I create a view into the container in. The adapter filter creates another view that only allows elements that satisfy the predicate. None of the views store