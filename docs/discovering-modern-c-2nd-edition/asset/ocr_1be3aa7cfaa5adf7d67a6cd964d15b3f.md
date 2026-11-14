Speaking of program robustness, functions in universally used libraries should never abort. If the function is used, for instance, to implement an autopilot, we would rather turn off the autopilot than have the entire program terminated (picture an aircraft whose system is rebooting during landing). In other words, when we do not know all application domains of a library, we cannot tell the consequences of a program abort.

Sometimes, the cause of a problem is not 100% certain in theory but sufficiently clear in practice. The access operator of a vector or matrix should check whether the index is in a valid range. In principle, an out-of-range index could originate from user input or a configuration file, but in practically all cases it comes from a program bug. Raising an assertion seems appropriate here. To comply with the robustness issue, it might be necessary to allow the user to decide between assertion and exception with conditional compilation (see §1.9.2.3).

# A.2.6 Binary I/O

Conversions from and to strings can be quite expensive. Therefore, it is often more efficient to write data directly in their respective binary representations into files. Nonetheless, before doing so it is advisable to check with performance tools whether file I/O is really a significant bottleneck of the application.

When we decide to go binary, we should set the flag `std::ios::binary` for impeding implicit conversions like adapting line breaks to Windows, Unix, or Mac OS. It is not the case that the flag makes the difference between text and binary files: binary data can be written without the flag and text with it. However, to prevent the before-mentioned surprises it is better to set the flag appropriately.

The binary output is performed with the `ostream`'s member function `write` and input with `istream::read`. The functions take a `char` address and a size as arguments. Thus, all other types have to be casted to pointers of `char`:

![](bbox=[0.13, 0.79, 0.38, 0.81])

```
int main (int argc, char* argv[])
{
    std::ofstream outfile;
    with_io_exceptions(outfile);
```