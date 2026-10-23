has completed. If an exception is thrown then the succeeding continuation can handle it in a try-catch block.

We take two examples. The first example is an implementation of the graph in Figure 29.1. The implementation is not exactly in one-to-one correspondence with the graph but it is clear what the code is doing (and we still get the value 42):

```
```cpp
double ParallelTaskContinuation(double a)
{
  // Parallel with futures in BOOST

  std::cout << "Parallel with future continuations \n";
  //       double b = F1(a);
  boost::future<double> b = boost::async([=]() { return F1(a); });

  double val = 10.0;
  boost::future<double> c = b.then([&val] (boost::future<double> f)
                                   {return f.get() + val; });

  double f = F3(c.get());

  return f; // a = 22 => f == 42
}
```
```

The second example is an application of function composition in mathematics:

```
```cpp
double ChainingContinuation()
{
  // Parallel with futures in BOOST, composing functions
  //   exp(sqrt(x*x));

  double x = 5.0;

  // Functions to be composed in a pipeline
  auto f1 = [](double x) { return x*x; };
  auto f2 = [](double x) { return std::sqrt(x); };
  auto f3 = [](double x) { return std::exp(x); };

  std::cout << "Parallel with future chaining continuations \n";
  boost::future<double> fut1 = boost::async([=]() { return f1(x); });

  boost::future<double> fut2 = fut1.then([=](boost::future<double> f)
                                         { return f2(x); });
  boost::future<double> fut3 = fut2.then([=](boost::future<double> f)
                                         { return f3(x); });

  return fut3.get(); // should be 148.413
}
```
```

This code can be described as implementing a simple data flow program.
This design approach can easily be extended and generalised to more complex cases.
Continuations registered using the `.then` function avoid blocking waits or wasting threads on