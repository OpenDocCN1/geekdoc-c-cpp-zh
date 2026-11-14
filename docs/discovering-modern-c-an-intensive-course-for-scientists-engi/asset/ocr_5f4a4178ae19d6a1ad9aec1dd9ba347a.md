+   - Thus, the return type is `transposed_view<const dense2D<float>> >`.
+   - The constructor parameter has type `const dense2D<float>&`.
+   - Likewise, the member ref is a `const dense2D<float>&`.

There remains the question why the non-const version of the operator is called despite our referring to a constant matrix. The answer is that the constancy of ref does not matter for the choice but whether or not the view object itself is constant. To ascertain that the view is also constant, we could write:

```
```
const transposed_view<const mtl::dense2D<float>> Bt(B);
cout << "Bt(2, 0) = " << Bt(2, 0) << '\n';
```
```

This works but is pretty clumsy. A brutal possibility to get the view compiled for constant matrices is to cast away the constancy. The undesired result would be that mutable views on constant matrices enable the modification of the allegedly constant matrix. This violates our principles so heavily that we do not even show what the code would look like.

> **Rule**
> Consider casting away const only as the very last resort.

In the following, we will empower you with very strong methodologies for handling constancy correctly. Every `const_cast` is an indicator of a severe design error. As Herb Sutter and Andrei Alexandrescu phrased it, “If you go const you never go back.” The only situation where we need `const_cast` is when we deal with const-incorrect third-party software, i.e., where read-only arguments are passed as mutable pointers or references. That is not our fault and we have no choice. Unfortunately, there are still many packages around that are entirely ignorant of the const qualifier. Some of them are too large for a quick rewrite. The best we can do about it is add an appropriate API on top of it and avoid working with the original API. This saves us from spoiling our applications with `const_cast`s and restricts the unespable `const_cast` to the interface. A good example of such a layer is `Boost::Bindings` [30] that provides a const-correct high-quality interface to BLAS, LAPACK, and other libraries with similarly old-fashioned interfaces (to phrase it diplomatically). Conversely, as long as we only use our own functions and classes we are able to avoid every `const_cast` with more or less extra work.

To handle constant matrices correctly, we could implement a second view class especially for constant matrices and overload the `trans` function to return this view for constant arguments:

```
```
template <typename Matrix>
class const_transposed_view
{
  public:
```
```