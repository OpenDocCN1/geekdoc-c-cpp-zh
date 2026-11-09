No, that would be absurd. We need a simpler approach. What if we use the law of trichotomy?

The law of trichotomy says that given two numbers A and B, there are only three possible relationships between them: A < B, A = B, or A > B. Okay, so let’s arbitrarily pick one of the elements of the list and then decide which of those relationships it has with the others.

The relevant code looks like this:

Click here to view code image

```
    else {
      int first = list.get(0);
      int middle = list.get(1);
      int last = list.get(2);
      List<Integer> lessers = new ArrayList<>();
      List<Integer> greaters = new ArrayList<>();

      if (first < middle)
        lessers.add(first);
      if (last < middle)
        lessers.add(last);
      if (first > middle)
        greaters.add(first);
      if (last > middle)
        greaters.add(last);

      List<Integer> result = new ArrayList<>();
      result.addAll(lessers);
      result.add(middle);
      result.addAll(greaters);
      return result;
    }
```

Now, don’t freak out. Let’s walk through this together.

First, we extract the three values into the three named variables: `first`, `middle`, and `last`. We do this for convenience because we don’t want a bunch of `list.get(x)` calls littering up the code.

Next, we create a new list for the elements that are less than the `middle` and another for the elements that are greater than the `middle`. Note that we are