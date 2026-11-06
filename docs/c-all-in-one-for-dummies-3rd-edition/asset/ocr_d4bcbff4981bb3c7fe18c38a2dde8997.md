because this map is holding pointers, *really* it's holding numbers, not instances — something to think about.

And so we next set up some instances and then made one association:

```
```
pointers[akey10] = &value10;
```
```

Note the use of the ampersand (&), which we used as a reference operator to help us store the addresses in `map`. Then we changed the `Item` member of one of the value objects:

```
```
value10.Item = 12345;
```
```

And this time, when we print it by using this carefully parenthesized line

```
```
cout << (*pointers[akey10]).Item << endl;
```
```

we see this:

```
```
12345
```
```

And once again . . . aha! This time the change stuck. Why is that? Because even though `map` holds a copy, it's holding a copy of a pointer. And that pointer happens to point to the original `value10` object. So when we changed the `Item` member of `value10`, `map` picked up the change. `map` itself didn't change, but `map` is pointing to that value.

![](bbox=[0.122, 0.566, 0.219, 0.636])

From all this discussion about the containers holding copies, you can come to the following conclusion. Because `map` holds copies, you can remember these two rules about deleting your original objects:

+   - **When the container holds instances:** If you're putting instances in `map`, you can delete the original instances after they're in `map`. This is okay because `map` has its own copies of the instances.
+   - **When the container holds pointers:** If you're putting pointers in `map`, you don't want to delete the original instances because the pointers in `map` still point to these instances.

So which method is best? It's up to you. But here are a couple of things to consider:

+   - **Keeping instances around:** If you don't want to keep instances lying around, you can put the instances in the container, and it will make copies.
+   - **Copyability:** Are your classes copyable? Some classes, such as classes filled with pointers to other classes or classes that are enormous, don't copy well. In that case, you may want to put pointers in the container.