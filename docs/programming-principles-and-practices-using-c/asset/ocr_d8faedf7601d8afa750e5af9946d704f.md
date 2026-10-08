![](bbox=[0.23, 0.07, 0.85, 0.42])

You can define an exception by deriving from a standard library exception like this:

```
struct My_error : runtime_error {
	My_error(int x) : interesting_value(x) { }
	int interesting_value;
	const char* what() const override { return "My_error"; }
};
```

# ## B.3 Iterators

Iterators are the glue that ties standard library algorithms to their data. Conversely, you can say that iterators are the mechanism used to minimize an algorithm’s dependence on the data structures on which it operates (§20.3):

![](bbox=[0.27, 0.72, 0.8, 0.89])