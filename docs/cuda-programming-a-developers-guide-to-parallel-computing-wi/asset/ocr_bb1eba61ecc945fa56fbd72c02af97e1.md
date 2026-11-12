overlapped. In the previous timeline this would cause, with some program changes, the copy-back-to-host transfers to occur while the copy-to-device transfers were occurring. In effect, we'd eliminate the time of the copy-back-to-host transfers, a significant savings. Due to both DMA engines being enabled on Tesla devices, enabling streams can bring significant benefits for this platform.

Note also that for this test we are using a PCI-E 2.0 X8 link. Using a PCI-E 3.0 X16 link would reduce the transfer time to around a quarter of what is shown here, making transfers less of an issue.

Once you have your kernel working, and only once you have it working, switch to an asynchronous mode of operation. An Asynchronous operation, however, can make debugging somewhat more complex so this is best done only once everything works correctly.

SDK Samples: Grabcut, Histogram Equalization, BoxFilter, Image Segmentation, Interoperability with the FreeImage library.

# Thrust

Those familiar with C++ may have used the C++ STL, and specifically the BOOST library. For those not familiar with templates, they are actually a very useful feature of C++. In traditional C If you have a simple function that you wish to perform an operation, sum for example, you have to specify the operand type explicitly. Thus, you might have something like the following:

```
int sum(const int x, const int y)
{
    return x+y;
}
```

If I wish to call the function and pass a float then I need a new function. As C does not allow the same name for two functions, I need something like sum_32f, sum_u8, sum_u32, sum_f32, etc. It's somewhat tedious to provide and use a library that is type specific.

C++ tried to address this in the form of function overloading. This allows the same name to be used for many functions. Depending on the type of the parameters passed, the appropriate function is called. However, the library provider still needs to write one function body to handle int8, int16, f32, etc. even if he or she can now use a common name for the function.

The C++ template system addresses this. We have a generic function that changes only in terms of the type of its parameters. Thus, why does the programmer have to copy and paste the code a dozen times to support all the possible permutations he or she might imagine? Templates, as the name suggests, mean supplying a template of what you'd like to do in a type agnostic manner. The compiler then generates a version of the function at compile time if, and only if, it is actually called.

Thus, the STL was born, a type agnostic definition of some very common functions in C++. If you happen to use the int32 version, but not the f32 version, only the int32 version results in actual code within your application. The downside of templates, as opposed to libraries, is that they are compiled during every compilation run, so they can increase compile times.

The NVCC compiler is actually a C++ front end, rather than a C front end. The standard development package on Windows, Microsoft Visual Studio, also supports C++ language, as do the primary Linux and Mac development environments.

The Thrust library supports many of the STL containers for which it makes sense to support on a massively parallel processor. The simplest structures are often the best and thus arrays (or vectors as