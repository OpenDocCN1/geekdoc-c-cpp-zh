```
```cpp
BOOST_AUTO_TEST_CASE( add_size_1 ) {
    using namespace std::literals::string_literals;
    qw::index inst{};                         // arrange
    inst.add( ""s);                          // act
    BOOST_CHECK_EQUAL(inst.size(), 1u);       // assert
}
BOOST_AUTO_TEST_CASE( normalize ) {
    using namespace std::literals::string_literals;
    qw::index inst{}; // arrange
    // acts and asserts; could also be in separate functions
    BOOST_CHECK_EQUAL(inst.normalize("a"), "a"s);
    BOOST_CHECK_EQUAL(inst.normalize("Town"s), "TOWN"s);
    BOOST_CHECK_EQUAL(inst.normalize("White Space"s), "WHITESPACE"s);
    BOOST_CHECK_EQUAL(inst.normalize("!Sym-bol.s"), "$YM#BOL#s");
}
BOOST_AUTO_TEST_CASE( move ) {
    qw::index inst{};
    qw::index other = std::move( inst );
    BOOST_CHECK_EQUAL(other.size(), 0u); // pimpl successfully moved?
}
```
```

**Listing 14.6** This test module tests qwort.cpp.

I start the includes with the header file of the module being tested—in this case, qwort/qwort.hpp. This makes the components to be tested known within this file.

Next are the includes of the test framework—here only one, namely, boost/test/included/unit_test.hpp. With this include, you have the option to automatically generate a main() function and a master test suite. The framework does this if you define the BOOST_TEST_MODULE macro before the include. You also give the test module a meaningful name—here, qwort. Note that you are allowed to define this macro at most once per test program before the include. Logically, it ensures that a main() function is generated, and there can only be exactly one per program.

After the using directive, the test cases follow. Each one is introduced by the macro BOOST_AUTO_TEST_CASE, given a descriptive name as a parameter, and otherwise has the form of a free function. The macro ensures that this free function is registered under the descriptive name in the master test suite, so that it is executed when the test program is run.

Within the test functions, I use the usual arrange, act, assert (AAA) pattern. In the assert section, I use the Boost macros from Table 14.1.

The tests here are not particularly complicated and are mostly self-explanatory. However, I would like to point out a few smaller things.