```
```cpp
}

TEST( DecRoman_TestSuite, ChainTest )
{
    bool result = Decimal_2_Roman_Chain_UnitTest();

    // Nonfatal assertion
    EXPECT_EQ( result, true ) << "All decimals 1..3999 should pass and vice versa";

    // Fatal assertion
    ASSERT_EQ( result, true ) << "All decimals 1..3999 should pass and vice versa";
}
```
```

The previous *test.cpp* source file is generated automatically by the project wizard when creating *RomanApp_GTest*, as shown in Figure A.12. It contains some predefined *Google Test* constructions. On line [1], the precompiled header is included through the *pch.h* file. This is a feature specific to the Microsoft Visual Studio platform, which for compatibility reasons we avoided in other projects presented in this book. Using the precompiled header can be switched off in the settings pane opened for the source file. Then, line [3] includes the *Dec2Roman.h* header, which lets us call the *Decimal_2_Roman_Chain_UnitTest* test function from the main *RomanApp* project. Therefore the name of the header is preceded by the relative path.

The TEST macro, which calls the EXPECT_EQ and EXPECT_TRUE macros on lines [5–7], was automatically added by the wizard to show very basic features of the *Google Test* platform. However, in the same fashion on line [11], we add our own test. First, on line [13], the *Decimal_2_Roman_Chain_UnitTest* test function is called, and the result of its operation is saved in the *result* flag. This is then checked by two assertions: the non-fatal EXPECT_EQ on line [16] and the fatal ASSERT_EQ on line [19]. This is all we need to run the test by pressing the green button in the Test Explorer pane, as shown in Figure A.14.

![](bbox=[0.135, 0.593, 0.875, 0.845])

**Figure A.14** Visual Studio with two projects: *RomanApp* and its *RomanApp_GTest* testing project, based on the Google Test library. Software unit tests are written using macros defined with Google Test. They call a unit test written to test the specific behavior of *RomanApp*. As shown in the Test Explorer pane, the first test from *test.cpp* passed, while the second one failed.