Line [63] in Listing 7.11 shows the `FxPt_Test_2` test function. Its main purpose is to exemplify the `const` and `constexpr` objects, as shown on lines [68–69]. We will again stress the difference: a `const` object behaves like all other runtime-created objects. Its only restriction is that, once created, it cannot be modified. Note that despite being a `const` object, the `static_assert` on line [72] will not compile, since the object is not a `constexpr` (hence this line is commented out). On the other hand, the `constexpr` object on line [69] is meant to be created before the whole translation unit is compiled. If this is possible, then the entire process will take place during compilation, and the resulting (also constant) object will be embedded into the resulting code. In this case, the `static_assert` on line [75] will be fulfilled – first, because it is a `constexpr` object; and second, because the condition is true.

```
```cpp
void FxPt_Test_2( void )
{
    // ------------------
    // const vs. constexpr

    const FX_8_8        d1 {};   // d1 will be const
    constexpr FX_8_8 d2 {};       // d2 will be const and computed during compilation

    // Will not compile - is not sufficient, must be constexpr
    // static_assert( d1.GetInternalValue() >= 0 );

    // This is ok
    static_assert( d2.GetInternalValue() >= 0 );
    // Will not compile - d2 is const FX_8_8
    // d2 *= 2.0;
}
```
```

An attempt on line [77] to modify the `d2` object will fail because `constexpr` on line [69] imposes const properties on the `d2` object.

# 7.4 Floating-Point Representations

Computers are commonly associated with computations. Computer-aided design systems, physical simulations, weather forecasting, cosmic flights, artificial intelligence, etc. – all these and many more are heavily based on mathematical procedures performed by computers. All require numerical value representations in a computer’s memory. We discussed integer and FX arithmetic in previous sections. However, if we think of doing computations with values ranging from, for example, −1500.13 up to 1.2e+12, we can see that the formats have a number of important limitations. A mechanism had to be invented for their efficient representation, which would also be compatible with various computer platforms. Such representations have been known at least for half a century in the form of the *floating-point* (FP) format. We have used it many times in the examples presented in this book.