This has the following effect:

```
Tracker track1{"track1:"};
Tracker track2{"track2:"};

std::pmr::string s1{"more than 15 chars", &track1};    // allocates with track1
std::pmr::string s2{std::move(s1), &track1};            // moves (same tracker)
std::pmr::string s3{std::move(s2), &track2};            // copies (different prefix)
std::pmr::string s4{std::move(s3)};                     // moves (allocator copied)
std::string s5{std::move(s4)};                          // copies (other allocator)
```

That is, moves are only performed as moves if the source and destination have interchangeable allocators. This is the case for polymorphic allocated types when the move constructor is used (the new object copied the allocator). However, if a non-interchangeable allocator is required (as with the tracker having a different prefix here) or if a different allocator type is used (as by moving to a std::string, which uses the default allocator), the memory is copied. Thus, interchangeability affects the performance of moves.

If we were to make all memory resources of type Tracker interchangeable by checking only the type:

```
bool do_is_equal(const std::pmr::memory_resource& other) const noexcept override {
    // all Tracker's are interchangeable if they have the same type:
    return this == &other || dynamic_cast<const Tracker*>(&other) != nullptr;
}
```

we would get the following behavior:

```
Tracker track1{"track1:"};
Tracker track2{"track2:"};

std::pmr::string s1{"more than 15 chars", &track1};    // allocates with track1
std::pmr::string s2{std::move(s1), &track1};            // moves (same tracker type)
std::pmr::string s3{std::move(s2), &track2};            // moves (same tracker type)
std::pmr::string s4{std::move(s3)};                     // moves (allocator copied)
std::string s5{std::move(s4)};                          // copies (other allocator)
```

As you can see, the effect would be that the memory allocated with track1 is passed via s3 to s4, which both use track2, so that we get:

```
track1:allocate 32 Bytes
track2:deallocate 32 Bytes
```

This would be a good implementation if our memory resource did not have different states (i.e., did not have the prefix), because this improves the performance of moves.

Therefore, it is worthwhile making memory resources interchangeable because fewer moves convert to copies. However, you should not make them more interchangeable than their purpose needs.