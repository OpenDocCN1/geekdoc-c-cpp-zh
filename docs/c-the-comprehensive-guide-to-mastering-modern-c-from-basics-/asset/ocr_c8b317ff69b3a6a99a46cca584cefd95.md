```
return nullptr;
}
```

# **Listing 14.7** The test suite is manually assembled here.

Now all functions that test the index_impl class have become methods of the ImplMultimapTest class. BOOST_AUTO_TEST_CASE does not help here; instead I define the init_unit_test suite function. Boost.Test usually takes care of this, but this I do not define BOOST_TEST_MODULE and have to write this function myself.

To be able to call the methods, I need an instance of the ImplMultimapTest class. This is done by the following line:

```
auto tester = std::make_shared<ImplMultimapTest>();
```

An instance is now available for the duration of the tests. The individual methods must be added to the framework::master_test_suite(), which is automatically processed by the Boost.Test framework.

This is how the methods get into this suite:

```
ts.add( BOOST_TEST_CASE([=](){ tester->METHOD(); } ) );
```

You could also use method pointers and std::bind here, but I find the lambda clearer.

Note that when you use a shared_ptr for the test class, it is not recreated for each test case. In this case, it is not critical, but to get the test class reinstantiated for each