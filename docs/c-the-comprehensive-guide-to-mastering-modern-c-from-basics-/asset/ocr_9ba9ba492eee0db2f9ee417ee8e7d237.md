takes a range as a parameter, you typically write it in a compact form like this:

```
void print(auto&& range) {
    for (const auto& elem : range) cout << elem << "\n";
}
```

Or, if you want to constrain the range to a suitable range concept, like this:

```
void print(ranges::input_range auto&& arg) {
    for (const auto& elem : range) cout << elem << "\n";
}
```

The type is specified with auto&&. The Auto stands for an abbreviated function template. This is definitely a win, because otherwise, we would have to write a complicated template header for every function that takes a range as a parameter. This way is much better, and we don't even notice that we are defining a template.

But why don't I write const auto&&? Why do I leave out const, and why do I use the (somewhat obscure) universal reference &&?

I had written something about caching views in the explanation for Table 25.2, especially for begin(). However, caching means that begin() modifies the view! Unfortunately, this is necessary to keep the cost of calling begin() low. The standard library promises that the amortized cost of begin() is O(1)—that is, the cost for multiple calls. Even if the first call costs O(n), caching