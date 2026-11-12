# Example:

```
template <typename T>
__global__ void Kern(T in) { in(); }

template <typename T>
void bar4(void)
{
  auto lam1 = [] __device__ { return 10; };
  kern<<<1,1>>>(lam1);
}

struct C1_t { struct S1_t { }; friend int main(void); };
int main()
{
  struct S1_t { };
  // Error: enclosing function for device lambda in bar4
  // is instantiated with a type local to main.
  bar4<S1_t>();

  // Error: enclosing function for device lambda in bar4
  // is instantiated with a type that is a private member
  // of a class.
  bar4<C1_t::S1_t>();
}
```

9. With Visual Studio 2013 and later Visual Studio host compilers, the enclosing function must have external linkage. The restriction is present because this host compiler does not support using the address of non-extern linkage functions as template arguments, which is needed by the CUDA compiler transformations to support extended lambdas.

10. An extended lambda has the following restrictions on captured variables:

+   * In the code sent to the host compiler, the variable may be passed by value to a sequence of helper functions before being used to direct-initialize the field of the class type used to represent the closure type for the extended lambda²³.
+   * A variable can only be captured by value.
+   * A variable of array type cannot be captured if the number of array dimensions is greater than 7.
+   * For a variable of array type, in the code sent to the host compiler, the closure type's array field is first default-initialized, and then each element of the array field is copy-assigned from the corresponding element of the captured array variable. Therefore, the array element type must be default-constructible and copy-assignable in host code.
+   * A function parameter that is an element of a variadic argument pack cannot be captured.
+   * The type of the captured variable cannot involve types that are either local to a function (except for closure types of extended lambdas), or are private or protected class members.
+   * For a `__host__ __device__` extended lambda, the types used in the return or parameter types of the lambda expression's `operator()` cannot involve types that are either local to a function (except for closure types of extended lambdas), or are private or protected class members.

23 In contrast, the C++ standard specifies that the captured variable is used to direct-initialize the field of the closure type.