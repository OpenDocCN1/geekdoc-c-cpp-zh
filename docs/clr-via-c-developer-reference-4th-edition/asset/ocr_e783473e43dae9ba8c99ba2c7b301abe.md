The UnsafeDimArrayAccess method is marked with the unsafe modifier, which is required
to use C#'s fixed statement. To compile this code, you'll have to specify the /unsafe switch when
inoking the C# compiler or select the Allow Unsafe Code checkbox on the Build tab of the Project
Properties pane in Microsoft Studio.

Obviously, the unsafe technique has a time and place when it can be used by your own code,
and there are three serious downsides to using this technique:

+   - The code that manipulates the unsafe array elements is more complicated to read and write when
which manipulates the elements using the other techniques because you are using C#'s fixed
statement and performing memory-address calculations.

+   - If you make a mistake in the calculation, you are accessing memory that is not part of the array. This can result in an incorrect calculation, corruption of memory, a type-safety violation,\and a potential security hole.

+   - Due to the potential problems, the CLR forbids unsafe code from running in reduced-security
environments (like Microsoft Silverlight).

# Unsafe Array Access and Fixed-Size Array

Unsafe array access is very powerful because it allows you to access:

+   - Elements within a managed array object that resides on the heap (as the previous section
dstrated),

+   - Elements within an array that resides on an unmanaged heap. The SecureString example in
Chapter 14, "Chars, Strings, and Working with Text," demonstrated using unsafe array access
an an array returned from calling the System.Runtime.InteropServices.Marshal class's
SecureStringToCoMemUnicode method.

+   - Elements within an array that resides on the stack's thread.

In cases where performance is extremely critical, you could avoid allocating a managed array
object on the heap and instead allocate the array on the stack's thread using C#'s stackalloc
statement (which works like C alloc function). The stackalloc statement can be used
to create a single-dimensional, zero-based array of value type elements, and the value type must
ot contain any reference type fields. You should think of this as allocating a block of memory
that you can manipulate using unsafe pointers, and therefore, you cannot pass the address of this
memory buffer to the vast majority of FCL methods. Of course, the stack-allocated memory (array)
will automatically be freed when the method returns; this is where we get the performance improve-
ment. Using this feature also requires you to specify the /unsafe switch to the C# compiler.