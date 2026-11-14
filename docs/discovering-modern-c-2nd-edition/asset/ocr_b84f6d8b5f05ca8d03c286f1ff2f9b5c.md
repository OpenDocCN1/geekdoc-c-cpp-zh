When f returns, the pointers are destroyed and the memory referred to by p2 is released (without ever being used). The second allocated memory block still exists since p from the main function is still referring to it.

If possible, a shared_ptr should be created with make_shared:

Click here to view code image

```
shared_ptr<double> p1 = make_shared<double>();
```

Then the internal and the user data are stored together in memory—as shown in Figure 1–2—and the memory caching is more efficient. make_shared also provides better exception safety because we have only one memory allocation. As it is obvious that make_shared returns a shared pointer, we can use automatic type detection (§3.4.1) for simplicity:

```
auto p1 = make_shared<double>();
```

We have to admit that a shared_ptr has some overhead in memory and run time. On the other hand, the simplification of our programs thanks to shared_ptr is in most cases worth some small overhead.

Further reading: For deleters and other details of shared_ptr see the library reference [40, §5.2], [62, §34.3.2], or an online reference.

![](bbox=[0.34, 0.57, 0.65, 0.75])

Figure 1–2: Shared pointer in memory after make_shared

# C++11 1.8.3.3 Weak Pointer