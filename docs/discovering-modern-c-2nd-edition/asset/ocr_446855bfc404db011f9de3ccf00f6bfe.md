![](bbox=[0.13, 0.08, 0.83, 0.47])

Figure 5-1: Memory hierarchy

# 5.3.2 An Expression Template Class

The purpose of Expression Templates (ET) is to keep the original operator notation without introducing the overhead induced by temporaries. The technique was independently discovered by Todd Veldhuizen and Daveed Vandevoorde.

```
=> c++11/expression_template_example.cpp
```

To avoid choosing between elegance and performance, we introduce a new class that represents the sum of two vectors (which are referred in the new class). The addition does not return a vector anymore, but an object of this new class:

Click here to view code image

```
template <typename T>
class vector_sum
{
```