d) Compare the accuracy and run-time performance of the methods in this exercise with those from Exercise 2.

# 4. (Quiz and Brainstorming, Review Questions)

We used some C++11 syntax in Section 15.3 (we have already discussed the syntax in this book). Specifically, we used the following keywords in the code: `final`, `override`, `virtual`, `default` and `explicit`.

Answer the following questions:

+   a) Why are they being used and what are the consequences of using them?
+   b) How would the same goals from part a) be realised in older versions of C++?
+   c) How useful are lambda functions compared to traditional function objects, free functions and member functions in terms of readability and maintainability?

# 5. (Creating Code)

Fill in the code that is needed for the producer–consumer functions that use an initialiser list in Section 15.5.4. Test your code.

# 6. (Alternative Design for a Generic Distribution Class, Brainstorming)

In Section 15.7 we created a generic *adapter* class for Boost statistical distributions. The Boost online documentation proposes a similar design of non-member functions:

```
template <class RealType>
class any_distribution
{
public:
    template <class Distribution>
        any_distribution(const Distribution& d);
};

// Get the cdf of the underlying distribution:
template <class RealType>
    RealType cdf(const any_distribution<RealType>& d, RealType x);
// etc....
```

Answer the following questions:

+   a) Create the above class and test it using the same examples that we used in this chapter.
+   b) Compare the two approaches in terms of ease of use, robustness and maintainability.