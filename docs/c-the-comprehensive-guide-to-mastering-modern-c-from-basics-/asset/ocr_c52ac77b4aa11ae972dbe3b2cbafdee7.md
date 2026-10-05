However, to use the "s suffix for literals, it must be stated somewhere:

```
using namespace std::literals::string_literals
```

Also, using namespace std would have worked, because literals and string_literals are inline namespaceS.

For demonstration purposes, I used BOOST_TEST twice at the beginning to demonstrate the macro.

And because a test program that runs without complaints makes one skeptical whether anything happened at all, I deliberately included a failing test:

```
BOOST_WARN_EQUAL(qw::version(), 2);
```

Because qw::version() returns the value 1, you should receive a warning when running the tests here. You should, of course, correct this test before publishing (sending to your team).

In this way, you list all test cases for the module. You compile this source file together with the qwort library and get an executable program:

| 14.5.3 Compile Test |

```
g++ -o testqwort.x testqwort.cpp -lwort -I../include -L../src/lib
```

In this form, you do not need a Boost library because the .../included/... variant is "header-only" and does not