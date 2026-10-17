
```c
PyTuple_SetItem(pArgs, 0, px);

PyTuple_SetItem(pArgs, 1, py);

PyTuple_SetItem(pArgs, 2, pz);

PyTuple_SetItem(pArgs, 3, PyLong_FromLong(n));

PyTuple_SetItem(pArgs, 4, p1);

PyTuple_SetItem(pArgs, 5, p2);

PyTuple_SetItem(pArgs, 6, p3);

PyTuple_SetItem(pArgs, 7, PyLong_FromLong(n3));

PyTuple_SetItem(pArgs, 8, PyFloat_FromDouble(xminp));

PyTuple_SetItem(pArgs, 9, PyFloat_FromDouble(xmaxp));

PyTuple_SetItem(pArgs,10, PyLong_FromLong(ioptx));

PyTuple_SetItem(pArgs,11, PyFloat_FromDouble(yminp));

PyTuple_SetItem(pArgs,12, PyFloat_FromDouble(ymaxp));

PyTuple_SetItem(pArgs,13, PyLong_FromLong(iopty));

PyTuple_SetItem(pArgs,14, PyFloat_FromDouble(fxmin));

PyTuple_SetItem(pArgs,15, PyFloat_FromDouble(fxmax));

PyTuple_SetItem(pArgs,16, PyFloat_FromDouble(fymin));

PyTuple_SetItem(pArgs,17, PyFloat_FromDouble(fymax));

PyTuple_SetItem(pArgs,18, PyUnicode_FromString(title));

Py_XINCREF(pArgs);

PyObject_CallObject(pFunc, pArgs);

Py_XDECREF(pArgs);

Py_DECREF(pFunc);

}
};
```

//==============================================================================

```c
void HistoBin(double xnew, double a, double b,
              double x[], double y[], int n, int iopt)
```

//------------------------------------------------------------------------------

// Bins data for a histogram to be plotted by function Plot (with sty = 4)

//

// `xnew` - new value to be binned
// `a`, `b` - limits of total binning interval
// `x[]`  - bin boundaries (`x[1] = a`, `x[n] = b`)
// `y[]`  - frequency of values in the bins: `y[i]` in [`x[i]`,`x[i+1)`), `i = 1,n-1`
// `n`    - number of bin boundaries
// `iopt` - option: 0 - zeros bins
//             1 - bins new value `xnew`
//             2 - normalizes histogram
//------------------------------------------------------------------------------

```c
{
    static double h, s;
    int i;
    if (iopt == 0) {                                   // initialize bins
        h = (b-a)/(n-1);                               // bin size
        for (i=1; i<=n; i++) {
            x[i] = a + (i-1)*h;                        // bin boundaries
            y[i] = 0.e0;
        }
    } else if (iopt == 1) {                            // bin new values
        i = (int) ((xnew-a)/h) + 1;                    // bin index
        if ((i >= 1) && (i < n)) y[i] += 1;            // increment bin value
    } else if (iopt == 2) {                            // normalize histogram
        s = 0e0;
        for (i=1;i<=n-1;i++) s += y[i];
        for (i=1;i<=n-1;i++) y[i] /= s;
    }
}
```

#endif
