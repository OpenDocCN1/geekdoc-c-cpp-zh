```
}
int NUMBER_OF_ITERATIONS = angles.size();
```

The code in Listing 27.4 shows how the value of C is computed.
This value can be precomputed, as it is not likely to vary.

# Listing 27.4: Computation of C.

```
double k = 1.0;
for (int i = 0; i < NUMBER_OF_ITERATIONS; ++i)
{
    k *= sqrt(1.0 + pow(4.0, -i));
}

int32 C = int32(1.0 / k * 0x01000000 + 0.5);
```

# Sine and Cosine

The code in Listing 27.5 uses the rotation mode to compute the
sine and cosine of an angle.

# Listing 27.5: Sine and cosine implementation.

```
void SineCosine(int32 a, int32& s, int32& c)
{
    c = C;    // Pre-multiply (1, 0) by C
    s = 0;
    Normalize(c, s, a);    // Adjust angle to the ra
    RotationMode(c, s, a, &c, &s);
}
```