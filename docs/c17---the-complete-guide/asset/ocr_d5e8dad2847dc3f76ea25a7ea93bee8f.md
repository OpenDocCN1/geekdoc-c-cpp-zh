```
std::cout << "random elem: " << s << '\n';
});
}
```

After initializing a vector with plenty of string values (value0, value1, ...), we initialize a random-number engine initialized with a random seed:

```
// initialize a Mersenne Twister engine with a random seed:
std::random_device rd;  // random seed (if supported)
std::mt19937 eng{rd()};  // Mersenne Twister engine
```

and a destination range:

```
// initialize destination range (must be big enough for 10 elements):
std::vector<std::string> subset;
subset.resize(100);
```

The call to sample() now copies (up to) 10 elements of the source range to the destination range:

```
// copy 10 randomly selected values from the source range to the destination range:
auto end = sample(coll.begin(), coll.end(),
                subset.begin(),
                10,
                eng);
```

The return value that end is initialized with contains the position behind the last randomly extracted element, which can be used afterwards to print the extracted elements:

```
// print extracted elements (using return value as new end):
for_each(subset.begin(), end,
    [] (const auto& s) {
        std::cout << "random elem: " << s << '\n';
    });
```

# 25.5 Afternotes

size(), empty(), and data() were first proposed by Riccardo Marcangelo in http://wg21.link/n4017. The finally accepted wording was formulated by Riccardo Marcangelo in http://wg21.link/n4280.

as_const() was first proposed by ADAM David Alan Martin and Alisdair Meredith in http://wg21.link/n4380. The finally accepted wording was formulated by ADAM David Alan Martin and Alisdair Meredith in http://wg21.link/p0007r1.

clamp() was first proposed by Martin Moene and Niels Dekker in http://wg21.link/n4536. The finally accepted wording was formulated by Martin Moene and Niels Dekker in http://wg21.link/p002501.

sample() was first proposed by Walter E. Brown in http://wg21.link/n3842. The finally accepted wording was formulated by Walter E. Brown in http://wg21.link/n3925.