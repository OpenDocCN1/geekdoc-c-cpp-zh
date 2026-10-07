Prefer auto in Many Cases.

Ex4: what is the type of val?

```
const int &get();

int main() {
    const auto &val = get();
}
```

Ex5: what is the type of val?

```
const int *get();

int main() {
    const auto &val = get();
}
```

Ex6: what is the type of val?

```
const int &get();

int main() {
    const auto &&val = get();
}
```

# Exercise: Build your experiment library

The above exercise is perfect for building into a set of experiments that are saved in your GitHub gists mentioned in C++ Is Not Magic