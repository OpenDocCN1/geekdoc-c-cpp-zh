```
std::cout << "\n\n";
std::cout << std::setprecision(precision);
for (int n = 0; n<number; ++n)
{
    std::cout << std::generate_canonical<T, bits>(gen) << ", ";
}
std::cout << "\n\n";
}
```

A test program is:

```
// Generate canonical
int number = 4;
CanonicalGenerator<double>(number, 16);

using boost::multiprecision::cpp_dec_float_50;
CanonicalGenerator<double>(number, 50);
```

Typical output is:

```
0.6443861122559016, 0.9267760353530851, 0.8461941290458814, 0.929694695848
9013,

0.80979306562688702086916237021796405315399169921875,
0.86959590730995528495839153038104996085166931152344,
0.6135122815448957878103897201071958989049530029297,
0.244033083049029708710975522831405512988567352294922,
```

The algorithm *independent_bits_engine* has input parameters for the type of the wrapped engine, the number of bits that the generated numbers should have and the type of the generated random numbers (should be unsigned integers). An example is:

```
std::random_device rd;
const std::size_t W = 32;
std::independent_bits_engine<std::mt19937, W, std::uint_fast64_t>
    generator(rd());

std::cout << "\n\n";
std::cout << std::setprecision(precision);
for (int n = 0; n<number; ++n)
{
    std::cout << generator() << ", ";
}
std::cout << "\n\n";

// Construct the underlying engine with a seed sequence
std::seed_seq seedSeq = { -1,0, 1 };
std::independent_bits_engine<std::mt19937, W, std::uint_fast64_t>
    generator2(rd());
std::cout << "\n\n";
```