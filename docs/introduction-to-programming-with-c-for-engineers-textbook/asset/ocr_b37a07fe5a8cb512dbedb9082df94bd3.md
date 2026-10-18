The `static_assert` on line [37] is fulfilled if the rounding error is less than a given threshold. An interesting testing benchmark is created here – by reducing the rightmost threshold value on line [37], we can trace the activity of the compiler. At some lower value of the threshold, say 0.00005, the condition is not fulfilled, and the `static_assert` fires. But this is a vivid sign that the compiler assessed the current state. Information about the object size, values of the computed circle areas, and the error are displayed on lines [40–44].

```
```cpp
static_assert( ComputeRoundingError( area_8_8, area_d ) < 0.005 );

// area_d and area_8_8 have been already precomputed in compilation
cout << "sizeof(double) = " << sizeof( double );
cout << ", area<double> = " << area_d << endl;
cout << "sizeof(FX_8_8) = " << sizeof( FX_8_8 );
cout << ", area<FX_8_8> = " << static_cast<double>( area_8_8 ) << endl;
cout << "Diff = " << ComputeRoundingError( area_8_8, area_d ) << endl;
```
```

Having computed the area of a circle, we go a little further and compute the volume of a cylinder on lines [48–60]. Again, we do this in the floating-point and FX domains. The volume is computed using `FX_8_8` objects on lines [51–52]. Here, at least two interesting functions are involved. The first is the product of two `FX_8_8` objects, from which the second object is locally converted to a temporary object by means of the `FX_8_8` constructor. The product is then converted back to double by the `static_cast` operator, which invokes the double converting operator.

Finally, on line [54], an `FX_8_8` object, previously created as `constexpr`, is copied into a normal runtime object of the larger `FX_16_16` type. Here the member template copy constructor from line [80] in Listing 7.1 is called. Then, on line [58], the area is multiplied by the height to obtain the cylinder’s volume, and the value is displayed.

```
```cpp
// --------------------------------------------------
// Compute at runtime

auto cyl_len { 1000.0 };

// There will be an overflow
cout << "volume<FX_8_8> = "
     << static_cast<double>( area_8_8 * FX_8_8( cyl_len ) ) << endl;

FX_16_16 area_16_16( area_8_8 );   // init wider from shorter

// Compute a volume of a cylinder
area_16_16 *= cyl_len;

cout << "volume<FX_16_16> = " << static_cast<double>( area_16_16 ) << endl;
}
```
```