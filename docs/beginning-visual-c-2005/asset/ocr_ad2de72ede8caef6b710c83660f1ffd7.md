# Chapter 18

If you plan to distribute program code in the form of a DLL for use by other programmers, you need to distribute all three files in the package. For applications that already use the DLL, just the .dll is required along with the .exe file.

# Exporting Variables and Functions from a DLL

You’ve seen how you can export classes from an extension DLL using the AFX_EXT_CLASS keyword. You can also export objects of classes that are defined in a DLL, as well as ordinary variables and functions. These can be exported from any kind of DLL by using the attribute dllexport to identify them. By using dllexport to identify class objects, variables or functions that are to be exported from a DLL, you avoid getting involved in the complications of modifying the .def file and, as a consequence, you make defining the interface to the DLL a straightforward matter.

Don’t be misled into thinking that the approach you’re taking to exporting things from your DLL makes the .def file method redundant. The .def file approach is more complicated — which is why you’re taking the easy way out — but it offers distinct advantages in many situations over the approach you’re taking. This is particularly true in the context of products that are distributed widely, and are likely to be developed over time. One major plus is that a .def file enables you to define the ordinals that correspond to your exported functions. This allows you to add more exported functions later and assign new ordinals to them, so the ordinals for the original set of functions remain the same. This means that someone using a new version of the DLL with a program built to use the old version doesn’t have to relink their application.

You must use the dllexport attribute in conjunction with the keyword _declspec when you identify an item to be exported. For example, the statement

```
_declspec(dllexport) double aValue = 1.5;
```

defines the variable aValue of type double with an initial value of 1.5 and identifies it as a variable that is to be available to programs using the DLL. To export a function from a DLL, you use the dllexport attribute in a similar manner. For example:

```
_declspec(dllexport) CString FindWinner(CString* Teams);
```

This statement exports the function FindWinner() from the DLL.

To avoid the slightly cumbersome notation for specifying the dllexport attribute, you can simplify it by using a preprocessor directive:

```
#define DllExport _declspec(dllexport)
```

With this definition, you can rewrite the two previous examples as:

```
DllExport double aValue = 1.5;
DllExport CString FindWinner(CString* Teams);
```

This notation is much more economical, as well as easier to read, so you may want to adopt this approach when coding your DLLs.