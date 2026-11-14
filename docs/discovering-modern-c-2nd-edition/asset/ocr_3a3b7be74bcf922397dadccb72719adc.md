```
static std::uniform_int_distribution<> d();
using param_t = decltype(d)::param_type;
return d(global_urng(), param_t(from, thru));
}
```

# double pick(double from, double upto)

```
{
    static std::uniform_real_distribution<> d{};
    using param_t = decltype(d)::param_type;
    return d(global_urng(), param_t(from, upto));
}
```

To start with random numbers, you could just copy these three functions into the project and look at the details later. Walter's interface is pretty simple but nonetheless sufficient for many practical purposes like code testing. We only need to remember the following three functions:

+   * `randomize`: Make the numbers really random by initializing the generator's seed.
+   * `pick(int a, int b)`: Give an `int` in the interval `[a, b]` when `a` and `b` are `int`.
+   * `pick(double a, double b)`: Give a `double` in the right-open interval `[a, b)` when `a` and `b` are `double`.

6. Walter used return type deduction of non-lambda functions which is only available in C++14 and higher. We further shortened the function name from `pick_a_number` to `pick`.

Without calling `randomize`, the sequence of generated numbers is equal each time which is desirable in certain situations: finding bugs is much easier with reproducible behavior. Note that `pick` includes the upper bound for `int` but not for `double` to be consistent with standard functions. `global_urng` can be considered as an implementation detail for the moment. With those functions, we can easily write loops for rolling dice:

Click here to view code image

```
randomize();
cout << "Now, we roll dice:\n";
for (int i = 0; i < 15; ++i)
    cout << pick(1, 6) << endl;

cout << "\nLet's roll continuous dice now: ;-)\n";
```