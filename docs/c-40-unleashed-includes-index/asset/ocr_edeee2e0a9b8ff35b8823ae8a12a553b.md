```
filter :: (a -> Bool) -> [a] -> [a]
filter _ []                 = []        -- empty list stays empty
filter p (x:xs) | p x       = x : filter p xs -- apply the filter to the head,
                | otherwise = filter p xs   -- keep the head if it passes
```

Don't worry too much about this syntax (unless you want to learn Haskell as well). The core idea is that the filter function takes in a predicate function that's evaluated for each element. Calling this on our list introduces a bit of "ceremony," though:

```
let evens = filter (\n -> (mod n 2) == 0) nums
```

Although this clearly shows the filter function that's being used, it's quite verbose syntax you have to stare at for every single filter you want to apply to a list. To mitigate this, Haskell introduced list comprehension syntax, which provides a more concise way to express the same:

```
let evens = [ n | n <- nums , (mod n 2) == 0]
```

Believe me, to a Haskell developer this looks quite sexy. But the same observation holds for LINQ: Although functions like filter (where in LINQ) are all you need to express rich queries, it gets aesthetically unpleasant pretty quickly. Having simplified syntax helps a lot to make the code more understandable and feel more natural. Let's build a similar query in LINQ with and without the query expression syntax:

```
var nums = new List<int> { 1, 2, 3, 4, 5 };

// Without query expression syntax
var evens = nums.Where(n => n % 2 == 0);

// With query expression syntax
var evens = from n in nums
			where n % 2 == 0
			select n;
```

Although the former syntax is all you need, it looks quite funky due to the syntactical noise that comes from dots, parentheses, and lambda arrows. The latter syntax means exactly the same (and indeed, it gets compiled into the former syntax) but feels more natural thanks to specialized keywords.

This example is still too trivial to see the true advantages of LINQ. As we proceed through our exploration of query expression syntax, we'll see cases where simple-looking queries turn into quite a bit of nontrivial code underneath. Such code involves lots of lambda expressions floating around in a sea of generic operator methods being called. Doing such things by hand typically leads to queries that aren't easy to understand, whereas query expression syntax looks way more natural.