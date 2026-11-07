```
count13 = std::count_if(numbers.begin(), numbers.end(),
    [](int x){return x % 13 == 0;});
cout << "Count of numbers divisible by 13: " << count13 << '\n';

return 0;
}
```

Here is a sample output:

```
Sample size = 39
Count of numbers divisible by 3: 15
Count of numbers divisible by 13: 6

Sample size = 3900
Count of numbers divisible by 3: 1305
Count of numbers divisible by 13: 302

Sample size = 390000
Count of numbers divisible by 3: 130241
Count of numbers divisible by 13: 29860
```

The output illustrates that one should not rely on statistics based on small samples.

# The Why of Lambdas

You may be wondering what need, other than the flowering of geekly expressionism, the lambda serves. Let’s examine this question in terms of four qualities: proximity, brevity, efficiency, and capability.

Many programmers feel that it is useful to locate definitions close to where they are used. That way, you don’t have to scan through pages of source code to find, say, what the third argument to a `count_if()` function call accomplishes. Also if you need to modify the code, all the components are close at hand. And if you cut and paste the code for use elsewhere, again all the components are at hand. From this standpoint, lambdas are ideal because the definition is at the point of usage. Functions are worst because functions cannot be defined inside other functions, so the definition will be located possibly quite far from the point of usage. Functors can be pretty good because a class, including a functor class, can be defined inside a function, so the definition can be located close to the point of use.

In terms of brevity, the functor code is more verbose than the equivalent function or lambda code. Functions and lambdas are approximately equally brief. One apparent exception would be if you had to use a lambda twice:

```
count1 = std::count_if(n1.begin(), n1.end(),
    [](int x){return x % 3 == 0;});
count2 = std::count_if(n2.begin(), n2.end(),
    [](int x){return x % 3 == 0;});
```