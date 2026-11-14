To see that the distributivity doesn't hold precisely, we can decrease eps to 0. Then, we see an (abbreviated) error message like

```
Test detected that (-6.21,7.09) * ((2.52,-3.58) + (-4.51,3.91))
!= (-6.21,7.09) * (2.52,-3.58) + (-6.21,7.09) * (-4.51,3.91)
terminate called after throwing 'distributivity_violated'
```

Now we go into the details of random number generation.

# 4.2.2.3 Engines

The library <random> contains two kinds of functional objects: generators and distributions. The former generate sequences of unsigned integers (the precise type is provided by each class's typedef). Every value should have approximately the same probability. The distribution classes map these numbers to values whose probability corresponds to the parameterized distribution.

Unless we have special needs, we can just use the default_random_engine. We have to keep in mind that the random number sequence depends deterministically on its seed and that each engine is initialized with the same seed whenever an object is created. Thus, a new engine of a given type always produces the same sequence, for instance:

```
void random_numbers()
{
    default_random_engine re;
    cout << "Random numbers: ";
    for (int i = 0; i < 4; ++i)
        cout << re << (i < 3 ? " , " : "");
    cout << '\n';
}
```

```
int main ()
{
    random_numbers();
    random_numbers();
}
```

yielded on the author's machine:

```
Random numbers: 16807, 282475249, 1622650073, 984943658
Random numbers: 16807, 282475249, 1622650073, 984943658
```

To get a different sequence in each call of random_numbers, we have to create a persistent engine by declaring it static:

```
void random_numbers()
{
    static default_random_engine re;
    ...
}
```

Still, we have the same sequence in every program run. To overcome this, we must set the seed to an almost truly random value. Such a value is provided by random_device: