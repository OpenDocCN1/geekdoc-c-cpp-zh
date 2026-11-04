```
string name = null;
```

![](bbox=[0.1, 0.15, 0.55, 0.32])

```
name = "Bart";
```

![](bbox=[0.12, 0.4, 0.78, 0.62])

# FIGURE 4.36 The null reference.

Unfortunately, opinions vary. Some say null indicates no value has been set; however, the answer is that there's no answer. Others overload the meaning to indicate situations where no value can be found or computed: It's impossible to formulate an answer. In my opinion, the latter interpretation should be avoided. Why? Null is simply not a good way to indicate errors. Better ways exist, such as returning a success/failure Boolean indicator or throwing exceptions. The absence of a value—which is what null is really about—may indicate an error, but it can equally be a valid situation.

Go back to the phone book example. Two fundamentally different conditions exist: Either the specified name can't be found or a blank entry exists. In the first case, we've caught an error; either input was invalid, or the phone book is incomplete. The second case did produce an answer, though; a user was found but no phone number is known. If null were returned in both cases, how would the caller distinguish what has happened? And consider what would happen when empty entries were initially not allowed in our phone book but we want to change that: All callers would have to be rewritten to account for the two possible interpretation of null.

This follows the idea of null as a proper value within the domain of a type.

# NOTE

System.Collections.Generic.Dictionary<TKey,TElement> is a generic collection type that supports our desired phone book semantics. Two methods exist to retrieve the value for a given key: Either an exception is thrown if the key is not found or a Boolean is returned to signal this condition to the user. Notice that the use of null doesn't appear in this picture at all, keeping it available as a proper value for use within the dictionary. We discuss collections extensively in Chapter 16, "Collection Types."