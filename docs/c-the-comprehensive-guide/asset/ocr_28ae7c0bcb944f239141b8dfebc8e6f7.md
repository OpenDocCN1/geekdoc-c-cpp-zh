The BOOST_CHECK_EQUAL macro has two parameters, which are compared using the Boost internal equal_impl function. This then either uses an appropriate overload for the comparison or falls back to ==, and the same for int, so that with int result and the

```
`BOOST_CHECK_EQUAL(result, 42);`
```

test, ultimately result==42 is executed. But how does it work with const char *res, and what does it look like here?

```
`BOOST_CHECK_EQUAL(res, "TEXT");`
```

If the macro simply used == here, it would fail because only the two pointers would be compared, not the contents of the C strings. Fortunately, the framework is smart enough to use a function template with a specialization for two const char* parameters. This way, it works for all parameters of the check macros.

In my comparisons, however, I specifically used the ""s suffix after "TOWN"s to create a string literal instead of a C string literal. For example, in

```
`BOOST_CHECK_EQUAL(inst.normalize("Town"s), "TOWN"s);`
```

the following would have been incorrect:

```
`BOOST_CHECK_EQUAL(inst.normalize("Town"s), "TOWN");`
```

Because then at runtime, the C string literal would first have to be converted into a string. However, I have now done this at compile time with "TOWN"s and ensured that the Boost internal specialization for comparing two string parameters is used instead of a const char* with a string. Although that would have worked as well, I find it logical not to require these conversions during tests if it is not absolutely necessary.

However, to use the ""s suffix for literals, it must be stated somewhere:

```
`using namespace std::literals::string_literals`
```

Also, using namespace std would have worked, because literals and string_literals are inline namespaces.

For demonstration purposes, I used BOOST_TEST twice at the beginning to demonstrate the macro.

And because a test program that runs without complaints makes one skeptical whether anything happened at all, I deliberately included a failing test:

```
`BOOST_WARN_EQUAL(qw::version(), 2);`
```

Because qw::version() returns the value 1, you should receive a warning when running the tests here. You should, of course, correct this test before publishing (sending to your team).