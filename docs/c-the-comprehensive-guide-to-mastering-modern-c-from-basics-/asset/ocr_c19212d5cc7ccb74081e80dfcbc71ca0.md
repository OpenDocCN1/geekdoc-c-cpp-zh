```
result.begin(), result.end());
}
```

# Listing 14.8 A test function with a parameter can be called with test data.

You must then not forget to add the test function to the test suite. To connect Boost.Test data from params with the testQgramify function, use the BOOST_PARAM_TEST_CASE macro:

```
ts.add(BOOST_PARAM_TEST_CASE(&testQgramify, params.begin(), params.end()));
```

You could also load the data from an external file. Boost.Test can also automatically generate dynamic datasets for you. If you are interested in that, read the Boost.Test documentation, under “Data-Driven Test Cases.”

> Don't Forget to Add to the Test Suite!

Actually, I prefer the explicit approach over the automagical one with the BOOST_AUTO_TEST_CASE macro.

However, the latter has a huge advantage: when writing a new test at one point in the source code, you can't forget to add it at another point in the code as well. You wouldn't believe how often it has happened to me that I add a new test, which is supposed to fail initially, run the test suite, and then wonder: “Why is it passing?” Quite simply, it's because I forgot to add the new test method to the test suite.