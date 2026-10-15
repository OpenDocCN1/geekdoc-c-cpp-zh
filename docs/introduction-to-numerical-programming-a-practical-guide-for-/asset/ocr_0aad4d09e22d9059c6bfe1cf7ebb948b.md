```
PyTuple_SetItem(pArgs, 7, PyFloat_FromDouble(fymin));
PyTuple_SetItem(pArgs, 8, PyFloat_FromDouble(fymax));
PyTuple_SetItem(pArgs, 9, PyUnicode_FromString(xtext));
PyTuple_SetItem(pArgs,10, PyUnicode_FromString(ytext));
PyTuple_SetItem(pArgs,11, PyUnicode_FromString(title));
Py_XINCREF(pArgs);

PyObject_CallObject(pFunc, pArgs);

Py_XDECREF(pArgs);
Py_DECREF(py);
Py_DECREF(px);
Py_DECREF(pFunc);
}

//================================================================================
void MultiPlot(double x[], double y[], double sig[], int n[],
    const char *col[], int sty[], int nplot, int maxint,
    double xminp, double xmaxp, int ioptx,
    double yminp, double ymaxp, int ipty,
    double fxmin, double f xmax, double fymin, double fymax,
    const char *xtext, const char *ytext, const char *title)
//--------------------------------------------------------------------------------
// Plots nplot real functions of one variable given by sets of (x,y) points.
// The coordinate sets are stored contiguously in the arrays x[] and y[].
// The x and y-domains are extended to fit at most maxint intervals
// expressible as d * 10^p, with d = 1, 2, 5 and p integer.
//
// x[]      - abscissas of tabulation points for all functions
// y[]      - ordinates of tabulation points
// sig[]    - error bars of the tabulation points (useful for sty == 4)
// n[]      - ending index for the individual plots (nmax = n[nplot])
// col[]    - plot color ("red", "green", "blue" etc.)
// sty[]    - plot style 0 - scatter plot with squares
//            1 - line plot; -1 - dashed line
//            2 - polar plot; -2 - dashed line
//            3 - drop lines
//            4 - error bars; -4 - including line plot
// nplot    - number of plots
// maxint   - max. number of labeling intervals
// ioptx    - 0 - resize x-axis automatically
//            1 - resize x-axis based on user interval [xminp,xmaxp]
// ipty     - 0 - resize y-axis automatically
//            1 - resize y-axis based on user interval [yminp,ymaxp]
// fxmin    - min fractional x-limit of viewport (0 < fxmin < f xmax < 1)
// f xmax   - max fractional x-limit of viewport
// fymin    - min fractional y-limit of viewport (0 < fymin < fymax < 1)
// fymax    - max fractional y-limit of viewport
// xtext    - x-axis title; for "None" - axis is not labeled
// ytext    - y-axis title; for "None" - axis is not labeled
// title    - plot title
//--------------------------------------------------------------------------------
{
    int i;
    PyObject *pFunc, *pArgs, *px, *py, *ps, *pn, *pcolor, *pstyle;

    pFunc = PyObject_GetAttrString(pModule,"MultiPlot");

    px = PyList_New(n[nplot]+1);                     // 0-offset arrays
```