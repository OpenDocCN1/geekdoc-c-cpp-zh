Click here to view code image

```
template <typename Value>
using vector= tensor<1, Value>;

template <typename Value>
using matrix= tensor<2, Value>;
```

When we print the output of the following lines:

Click here to view code image

```
std::cout << "The type of vector<float> is "
          << typeid(vector<float>).name() << ".\n";
std::cout << "The type of matrix<float> is "
          << typeid(matrix<float>).name() << ".\n";
```

In a name demangler, we will see:

Click here to view code image

```
The type of vector<float> is tensor<1u, float>.
The type of matrix<float> is tensor<2u, float>.
```

Resuming, if you have experience with typedef, you will appreciate the new opportunities in C++11, and if you are new to type definitions, you should start with using right away.

# ## 3.5 Template Specialization

On the one hand, it is a great advantage that we can use the same implementation for many argument types. For some argument types we may, however, know a more efficient implementation, and this can be realized in C++ with Template Specialization. In principle, we could even implement an entirely different behavior for certain types at the price of utter confusion. Thus, the specialization shall be more efficient but behave the same. C++ provides enormous flexibility, and we as programmers are in charge of using this flexibility responsibly and of being consistent with ourselves.

# ### 3.5.1 Specializing a Class for One Type