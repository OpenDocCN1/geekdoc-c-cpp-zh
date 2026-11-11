# Creating a future in the current standard

```
```cpp
std::promise<std::string> p;
std::future<std::string> fut = p.get_future();
p.set_value("hello");
```
```

This may change with the function `std::make_ready_future` concurrently TS v1.

# Creating a future in the concurrency TS v1

```
```cpp
std::future<std::string> fut = make_ready_future("hello");
```
```

Using future and non-future arguments would make our job even more comfortable.

# Using future and non-future arguments

```
```cpp
bool f(std::string, double, int);
```
```

```
```cpp
std::future<std::string> a = /* ... */;
std::future<int>     c = /* ... */;

std::future<bool> d1 = when_all(a, make_ready_future(3.14), c).then(f);
// if(a.get(), 3.14, c.get())

std::future<bool> d2 = when_all(a, 3.14, c).then(f);
// if(a.get(), 3.14, c.get())
```
```

Neither the syntactic form d1 nor the syntactic form d2 is possible with the concurrency ts v1.

# 7.2.2 Five New Concepts

There are five new concepts for futures and promises in proposal 1054R0<sup>19</sup>.

+   - **FutureContinuation**, invocable objects that are called with the value or exception of a future as an argument.
+   - **SemiFuture**, which can be bound to an executor, an operation that produces a `ContinuableFuture` (`f = sf.via(exec)`).
+   - **ContinuableFuture**, which refines SemiFuture and instances can have one `FutureContinuation` attached to them (`f.then(c)`), which is executed on the future’s associated executor when the future becomes ready.
+   - **SharedFuture**, which refines `ContinuableFuture` and instances can have multiple `FutureContinuations` attached to them.
+   - **Promise**, each associated with a future and makes the future ready with either a value or an exception.

The paper also provides the declaration of these new concepts.

<sup>19</sup> http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1054r0.html