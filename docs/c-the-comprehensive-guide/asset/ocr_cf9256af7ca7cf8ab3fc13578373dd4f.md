```
```cpp
// https://godbolt.org/z/hee331WGe
unordered_set nums{ 1,2,3,4,5,6,7,8,9,10 };
cout << nums;             // Output similar to: 9 1 2 3 4 5 6 7 8 10
auto it = nums.begin();
while(it != nums.end()) {
    if(*it % 2 == 0) {   // even number?
        it = nums.erase(it); // Remaining elements do not change order
    } else {
        ++it;
    }
}
cout << nums;             // Output similar to: 9 1 3 5 7
```
```

**Listing 24.81** Deleting preserves the order of the remaining elements.

Even if the order of the output may look different on your computer, you will get the same order in the second output as in the first, just without even numbers.

The call to `erase` returns an iterator to the next element. If `erase` is not to be called, then `++it` ensures the iterator moves forward.

# ### Specialty: By the Bucketful

You can take a closer look at the contents of the individual buckets:

+   - With `bucket_count()`, you get the current number of buckets in the container. The number cannot exceed `max_bucket_count()`.
+   - `begin(int)` and `end(int)` provide you with iterators to the elements of a single bucket.
+   - Beforehand, you can check the number of elements in a single bucket with `bucket_size(int)`.
+   - With `int bucket(Key)`, you can find out which bucket an element would end up in.

I find it difficult to imagine a meaningful application for this deep interface. However, I can imagine that such insights can be useful when you have to deal with the disadvantage of unordered containers, which do not offer any time guarantees. I can only provide you with an example that lists the contents of the individual buckets of an *unordered_set* with curious eyes.

```
```cpp
// https://godbolt.org/z/39v4aqgd1
// Fill with 100 values
unordered_set<int> d{};
d.rehash(10);               // try to have 10 buckets
d.max_load_factor(100.0);   // 100 elements per bucket are okay
cout << "Bucket count: " << d.bucket_count() << '\n';
```
```