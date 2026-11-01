```
int b = 0;
int c = 0;
};

std::array<Agg, 100> a;

void fn(Agg&);
int main() {
  auto t = Agg{};
  fn(t);
  for (int i = 0; i < 1000; ++i) { // Fill the
array
    a[i] = t;
  }
}
```

std::fill will do this for you, though, so there is less code to read, and you are less likely to insert a bug as happened above. (Did you see that? Check the size of the array and the iteration count of the for loop.)

Click here to view code image

```
int main() {
  auto t = Agg{};
  fn(t);
  std::fill(std::begin(a), std::end(a), t); //
Fill the array
}
```

Compiler writers go to a lot of effort to generate the best code possible. The typical implementation of std::fill will include SFINAE machinery (or, more likely now, requires clauses) to enable a simple memcpy for trivially constructible and trivially copyable types where memset is safe and constructor invocation is not necessary.