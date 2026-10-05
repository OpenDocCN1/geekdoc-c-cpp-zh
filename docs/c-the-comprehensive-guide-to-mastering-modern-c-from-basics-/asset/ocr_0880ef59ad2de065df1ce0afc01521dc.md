| Macro BOOST_level... | Description |
|---|---|n| BOOST_FAIL(msg) | Aborts the current test. |
| BOOST_IS_DEFINED(sym) | True if the macro sym is defined. |

**Table 14.1** A brief overview of all assert macros in Boost.Test.

# # The Universal Macro BOOST_TEST

In the current Boost versions, there is the all-rounder BOOST_TEST. This macro takes a comparison as the first parameter and can optionally take **test manipulators** as additional parameters. This allows you to influence the precision or logging behavior. 

Thus, the following tests:

```
BOOST_REQUIRE_EQUAL(qw::version(), 1);
BOOST_REQUIRE_GT(qw::version(), 5);
BOOST_REQUIRE_CLOSE(a+0.1, b-0.8, 0.01);
```

perform the same task as the following:

```
BOOST_TEST(qw::version() == 1);
BOOST_TEST(qw::version() >= 5);
BOOST_TEST(a+0.1 == b-0.8, boost::test_tools::tolerance(0.01));
```

With this macro, the tests look more uniform, and the optional manipulators allow for more combinations and influence on the test behavior.

Since 1.59 (Boost.Test v3), the macro has been available. Systems from around 2017 should be able