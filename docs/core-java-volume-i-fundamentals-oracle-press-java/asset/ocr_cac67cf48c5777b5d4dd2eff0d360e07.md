The empty string "" is a string of length 0. You can test whether a string is empty by calling

```
    if (str.length() == 0)
```

or

```
    if (str.equals(""))
```

An empty string is a Java object which holds the string length (namely, 0) and an empty contents. However, a `String` variable can also hold a special value, called `null`, that indicates that no object is currently associated with the variable. (See Chapter 4 for more information about `null`.) To test whether a string is `null`, use

```
    if (str == null)
```

Sometimes, you need to test that a string is neither `null` nor empty. Then use

```
    if (str != null && str.length() != 0)
```

You need to test that `str` is not `null` first. As you will see in Chapter 4, it is an error to invoke a method on a `null` value.

# ### 3.6.6 Code Points and Code Units

Java strings are sequences of `char` values. As you saw in Section 3.3.3, “The `char` Type,” on p. 43, the `char` data type is a code unit for representing Unicode code points in the UTF-16 encoding. The most commonly used Unicode characters can be represented with a single code unit. The supplementary characters require a pair of code units.

The `length` method yields the number of code units required for a given string in the UTF-16 encoding. For example: