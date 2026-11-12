# Example:

```
```cpp
namespace N1 {
  struct S1_t {
    template <typename T> void foo(T);
  };
}

namespace N2 {
  template <typename T> int foo(T);

  template <typename T> void doit(T in) { foo(in); }
}

void bar(N1::S1_t in)
{
  /* extended __device__ lambda. In the code sent to the host compiler,
     this is replaced with the placeholder type instantiation expression
     '__nv_dl_wrapper_t< __nv_dl_tag<void (*)(N1::S1_t in), (lbar).1> > ()'
  */

  // As a result, the namespace 'N1' participates in ADL lookup of the
  /* call to "foo" in the body of N2::doit, causing ambiguity.
  */
  auto lam1 = [] __device__ () {};
  N2::doit(lam1);
}
```
```

In the example above, the CUDA compiler replaced the extended lambda with a placeholder type that involves the N1 namespace. As a result, the namespace N1 participates in the ADL lookup for foo(in) in the body of N2::doit, and host compilation fails because multiple overload candidates N1::foo and N2::foo are found.