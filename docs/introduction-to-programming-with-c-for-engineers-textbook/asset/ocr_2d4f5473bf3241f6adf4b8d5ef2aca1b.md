This is harnessed to the automated `Decimal_2_Roman_Chain_UnitTest`. It takes each randomly generated decimal value, converts it into a Roman numeral and then back into a decimal value, and compares the results:

```
////////////////////////////////////////////////////////////
// Unit test to randomly test both conversions
////////////////////////////////////////////////////////////
//
// INPUT:
//          kFrom, kTO - range of values to test
//          kNumOfTrials - a number of random test values
// OUTPUT:
//          true if all tests passed ok, false otherwise
//
// REMARKS:
//          Calls assert()
//

bool Decimal_2_Roman_Chain_UnitTest( const int kFrom = 1, const int kTo = 3999,
                                      const int kNumOfTrials = 1000 )
{
    // Check each random decimal if it converts ok
    for( const auto & val : CreateRandomVector( kFrom, kTo, kNumOfTrials ) )
        if( ConvertRoman_2_DecimalNumber( ConvertDecimal_2_RomanNumber(val) ) != val )
            return false; // test failed, exiting ...
    return true; // if here, then we passed all tests ;)
}
```

All of the programming techniques used in `Decimal_2_Roman_Chain_UnitTest` should be clear at this point. Note that in the `for` loop, `CreateRandomVector` function is called and returns a temporary object containing random values that are immediately used in the loop. This is a common technique and, thanks to the move semantics, it does not cause large computational overhead due to unnecessary copying of temporary objects. This is further discussed in Section 4.6.4.

So far, we have written test functions to test two concrete functions. In practical software projects, we will face dozens of functions, classes, components, libraries, etc. Therefore a more versatile unit test framework can be very helpful. The most popular are Google Test (Google 2019); Boost.Test (Rozental and Enficiаud 2019), Catch2 (Catch Org 2019); and the latest Microsoft Visual Studio, which comes with unit testing features (Augustin 2019). For more, see Section 9.7.

# 3.18  Example Project – Building a Currency Calculator Component

Exchanging currencies is a common financial operation in international trading. In this example, we will develop a simple program to perform currency exchanges. As shown in the software development diagram in Figure 2.4, let’s start by specifying our requirements. Actually, there is only one, and it is very simple:

+   - The program will let us exchange a value in one currency for a corresponding value of another currency, based on an exchange rate acquired from a currency exchange authority