
```java
assertEquals(asList(1, 2), sort(asList(2, 1)));
```

To make this pass, we’re going to have to do something marginally intelligent. If the input array has more than one element in it and the first two elements of the array are out of order, then we should swap them:

```java
private List<Integer> sort(List<Integer> list) {
    if (list.size() > 1) {
        if (list.get(0) > list.get(1)) {
            int first = list.get(0);
            int second = list.get(1);
            list.set(0, second);
            list.set(1, first);
        }
    }
    return list;
}
```

Maybe you can see where this is headed. If so, don’t spoil the surprise for everyone else. Also, remember this moment—we’ll be returning to it in the next section.

The next two tests pass already. In the first test, the input array is already in order. In the second test, the first two elements are out of order, and our current solution swaps them.

```java
assertEquals(asList(1, 2, 3), sort(asList(1, 2, 3)));
assertEquals(asList(1, 2, 3), sort(asList(2, 1, 3)));
```

The next failing test is three elements with the second two out of order:

```java
assertEquals(asList(1, 2, 3), sort(asList(2, 3, 1)));
```

We get this one to pass by putting our compare and swap algorithm into a loop that walks down the length of the list:

```java
        }
      }
    }
    return list;
    }
```

To finish this off, let’s do a larger-scale test:

```java
    assertEquals(
            asList(1, 1, 2, 3, 3, 3, 4, 5, 5, 5, 6, 7, 8, 9, 9,
    9),
            sort(asList(3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5, 8, 9, 7,
    9,
                        3)));
```

This passes, so our sort algorithm appears to be complete.

Where did this algorithm come from? We did not design it up front. It just came from the set of small decisions we made in order to get each failing test to pass. It was an incremental derivation. Voila!

And what algorithm is this? *Bubble sort*, of course—one of the worst possible sorting algorithms.

So maybe TDD is a really good way to incrementally derive really bad algorithms.

## Sort 2

Let’s try this again. This time we’ll choose a slightly different pathway. And again, view the video if possible, but then continue reading from this point.

Watch related video: SORT 2

Access video by registering at informit.com/register

We begin as we did before with the most degenerate tests possible and the code that makes them pass:

```java
public class SortTest {
    @Test
    public void testSort() throws Exception {
        assertEquals(asList(), sort(asList()));
        assertEquals(asList(1), sort(asList(1)));
        assertEquals(asList(1, 2), sort(asList(1, 2)));
    }
    private List<Integer> sort(List<Integer> list) {
        return list;
    }
}
```

As before, we then pose two items out of order:

```java
assertEquals(asList(1, 2), sort(asList(2, 1)));
```

But now, instead of comparing and swapping them within the input list, we compare and create an entirely new list with the elements in the right order:

```java
private List<Integer> sort(List<Integer> list) {
    if (list.size() <= 1)
        return list;
    else {
        int first = list.get(0);
        int second = list.get(1);
        if (first > second)
            return asList(second, first);
        else
            return asList(first, second);
    }
}
```

This is a good moment to pause and reflect. When we faced this test in the previous section, we blithely wrote the compare and swap solution as though it were the only possible way to pass the test. But we were wrong. In this example, we see another way.

This tells us that from time to time we may encounter failing tests that have more than one possible solution. Think of these as forks in the road. Which fork should we take?

Let’s watch how this fork proceeds.

The obvious next test is, as it was before, three elements in order:

```java
assertEquals(asList(1, 2, 3), sort(asList(1, 2, 3)));
```

But unlike in the previous example, this test fails. It fails because none of the pathways through the code can return a list with more than two elements. However, making it pass is trivial:

```java
private List<Integer> sort(List<Integer> list) {
  if (list.size() <= 1)
    return list;
  else if (list.size() == 2) {
    int first = list.get(0);
    int second = list.get(1);
    if (first > second)
      return asList(second, first);
    else
      return asList(first, second);
  } else {
    return list;
  }
}
```

Of course, this is silly, but the next test—three elements with the first two out of order—eliminates the silliness. This obviously fails:

```java
assertEquals(asList(1, 2, 3), sort(asList(2, 1, 3)));
```

How the devil are we going to get this to pass? There are only two possibilities for a list with two elements, and our solution exhausts both of those possibilities. But with three elements, there are *six* possibilities. Are we really going to decode and construct all six possible combinations?

No, that would be absurd. We need a simpler approach. What if we use the law of trichotomy?

The law of trichotomy says that given two numbers A and B, there are only three possible relationships between them: A < B, A = B, or A > B. Okay, so let’s arbitrarily pick one of the elements of the list and then decide which of those relationships it has with the others.

The relevant code looks like this:

```java
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

Next, we create a new list for the elements that are less than the `middle` and another for the elements that are greater than the `middle`. Note that we are assuming the `middle` is unique in the list.

Then, in the four subsequent `if` statements, we place the `first` and `last` elements into the appropriate lists.

Finally, we construct the `result` list by placing the `lessers`, the `middle`, and then the `greaters` into it.

Now you may not like this code. I don't much care for it either. But it works. The tests pass.

And the next two tests pass as well:

```java
assertEquals(asList(1, 2, 3), sort(asList(1, 3, 2)));
assertEquals(asList(1, 2, 3), sort(asList(3, 2, 1)));
```

So far, we've tried four of the six possible cases for a list of three unique elements. If we had tried the other two, `[2,3,1]` and `[3,1,2]`, as we should have, both of them would have failed.

But due either to impatience or oversight, we move on to test a list with four elements:

```java
assertEquals(asList(1, 2, 3, 4), sort(asList(1, 2, 3, 4)));
```

This fails, of course, because the current solution assumes that the list has no more than three elements. And, of course, our simplification of `first`, `middle`, and `last` breaks down with four elements. This may make you wonder why we chose the `middle` as element 1. Why couldn't it be element 0?

So, let's comment out that last test and change middle to element 0:

```java
int first = list.get(1);
int middle = list.get(0);
int last = list.get(2);
```

Surprise—the `[1,3,2]` test fails. Can you see why? If `middle` is 1, then the 3 and 2 get added to the `greaters` list in the wrong order.
