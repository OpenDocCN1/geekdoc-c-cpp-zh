So there is a possibility of error, which we have represented by the exception **bad_from_string**. In \S23.9, we demonstrate how **from_string()** (or an equivalent function) is essential for serious text processing because we need to extract numeric values from text fields. In \S16.4.3, we saw how an equivalent function **get_int()** was used in GUI code.

Note how **to_string()** and **from_string()** are similar in function. In fact, they are roughly inverses of each other; that is (ignoring details of whitespace, rounding, etc.), for every “reasonable type **T**” we have

```
s==to_string(from_string<T>(s))    // for all s
```

and

```
t==from_string<T>(to_string(t))    // for all t
```

Here, “reasonable” means that **T** should have a default constructor, a >> operator, and a matching << operator defined.

Note also how the implementations of **to_string()** and **from_string()** both use a **stringstream** to do all the hard work. This observation has been used to define a general conversion operation between any two types with matching << and >> operations:

```
template<typename Target, typename Source>
Target to(Source arg)
{
    stringstream interpreter;
    Target result;
    if (!(interpreter << arg)                    // write arg into stream
        || !(interpreter >> result)              // read result from stream
        || !(interpreter >> std::ws).eof())      // stuff left in stream?
            throw runtime_error("to<>() failed");
    return result;
}
```

The curious and clever !(interpreter>>std::ws).eof() reads any whitespace that might be left in the **stringstream** after we have extracted the result. Whitespace is allowed, but there should be no more characters in the input and we can check that by seeing if we are at “end of file.” So if we try to read an **int** from a **string**, both **to<int>("123")** and **to<int>("123 ")** will succeed, but **to<int>("123.5")** will not because of that last **_5**.