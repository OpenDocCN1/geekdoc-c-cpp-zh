distribution with the desired quality, as per the preceding example:

```
auto number = d6(engine);
```

And number is now between something between θ and 5 (inclusive) with equal probability. If you don't like having to always carry and specify the engine here, simply combine both into a function object—for example, with a lambda:

```
auto d = [&6]() { return d6(engine); };
std::cout << d() << '\n';
```

And when I run Listing 28.17 again, I get the output. And again and again—that's a very unlikely coincidence, isn't it? It would be indeed, but all engines (except one, which we will get to shortly) are pseudorandom number generators: initialized with the same seed, they always produce the same bit sequence—which looks random under certain considerations and is sufficient for many (most?) applications. The reason I always got the exact sequence of pseudorandom numbers is that I always chose the same seed for the engine—namely, the default value. You can pass a different seed as a constructor argument:

```
std::default_random_engine engine(42);
std::default_random_engine engine(806699);
std::default_random_engine engine(time(0)); // from <ctime>
```

Each seed value provides different pseudo-random sequence. If you start with a variable value—like here