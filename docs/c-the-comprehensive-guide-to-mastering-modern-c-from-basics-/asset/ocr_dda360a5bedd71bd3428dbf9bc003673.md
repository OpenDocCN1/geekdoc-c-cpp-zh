```
std::vector<Image> collection = loadCollection(false);
}
```

# **Listing 16.20** The class probably contains large amounts of data that are expensive to copy. But what is being copied here?

I have written a sample data type Image that likely holds large amounts of data in data . The compiler-generated operations for copy and assignment will completely copy this data field from the source to the target. So the data is duplicated after copying: I expect that, and thus it is fine.

Does it surprise you, then, when I tell you that at no point in Listing 16.20 are image duplicated in data ? If not, then you either have already read something about move operations or expect too much from C++. I would like to illustrate how duplicate data could exist due to copying, and explain why this is not the case here:

+   - With Image{"MonaLisa.png"}, I create a new Image including its data. The push_back of vector takes its Image and places it where it stores its own data. This is a good candidate for a complete copy.

+   - With return result; I return the vector by value. What was previously a local variable is to be passed outside. In this case, it should be stored in another variable with collection = ... Such a scenario is another very good candidate for a copy—which here would be the copy of all vector-Image elements.

A vector has its own area where it stores its data. The new Image instances within loadCollection() are, of