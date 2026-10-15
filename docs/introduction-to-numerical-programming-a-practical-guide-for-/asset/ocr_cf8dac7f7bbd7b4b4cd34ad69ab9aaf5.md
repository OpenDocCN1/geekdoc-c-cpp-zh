# Listing C.2  Calling Python Functions with Scalar Arguments from C++ Code (C/C++ Coding)

```
```cpp
// Calling Python functions with scalar arguments from C++ code
#include <iostream>
#include <Python.h>

int main()
{
    PyObject *pModule, *pFunc, *pArgs, *pValue;  // pointers to Python objects
    double x, y;

    x = 2.0; y = 3.0;                                      // values to be added

    Py_Initialize();                                       // initialize Python
                                                          // import module "operations.py"
    pModule = PyImport_Import(PyUnicode_FromString("operations"));
    if (!pModule) std::cout << "Failed to load <operations.py>";
                                                          // get reference to function Sum
    pFunc = PyObject_GetAttrString(pModule, "Sum");

    pArgs = PyTuple_New(2);                               // define tuple of 2 arguments
    PyTuple_SetItem(pArgs, 0, PyFloat_FromDouble(x));       // set 1st argument
    PyTuple_SetItem(pArgs, 1, PyFloat_FromDouble(y));       // set 2nd argument

    pValue = PyObject_CallObject(pFunc, pArgs);             // call Python function

    std::cout << x << " + " << y << " = " << PyFloat_AsDouble(pValue);

    Py_DECREF(pArgs);                                      // clean up
    Py_DECREF(pFunc);
    Py_DECREF(pModule);

    Py_Finalize();                                         // finish Python
}
```
```

The tuple of arguments to be passed to the Python function is populated with the help of the PyTuple_SetItem method. The conversion from the C/C++ type double to the float type of Python is accomplished by the function PyFloat_FromDouble.

The actual call of the Python function Sum is carried out by PyObject_CallObject, having as arguments the function object pFunc and the argument list pArgs. Before any further use, the returned value, pValue, needs to be converted into the type double by a call to PyFloat_AsDouble.

In the spirit of object-oriented programming, it is essential to dispose of all the Python objects in reversed order of their creation, and this is done by means of the Py_DECREF method. Finally, the Python interpreter is released by calling Py_Finalize().

Similar in concept, the program C.3 differs in that one of the arguments of the called function, Average, is a vector. To account for this difference, an additional pointer px to a Python list is created. The list is effectively allocated with PyList_New and its items are set by the method PyList_SetItem.

For a Python function, say Sum, to be conveniently used in a C/C++ program, it needs to be interfaced by a wrapper function meant to hide all the communication details (Listing C.3). The robust way to implement such a mechanism is actually by way of two C++ classes, namely a wrapper class for the