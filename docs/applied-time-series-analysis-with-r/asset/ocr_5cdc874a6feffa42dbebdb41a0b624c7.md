Example: The Wigner–Ville plot shown in Figure 12.4b for the twsoe
data set chirp (shown in Figure 12.2a) is obtained using the follow-
commands

```
data(chirp)
```

```
wv.wge(chirp)
```

The following commands are be used in conjunction with
dwt and mra functions in the CRAN package waveslim.
b plotts.dwt.wge(x,n.levels,type)

This function calculates the dwt, outputs the wavelet coefficients,
plots the DWT in the format of Figure 12.7, and optionally plots the
ogram (time-scale plot)

x is the realization to be analyzed (x must be a vector of length
length 2^j₀ for some positive integer j₀ between 2 and 14.
n.levels (default = 4) is the number of levels (n.levels ≤ j₀)
type specifies the type of wavelet used (default = S8), i.e.
Symlet(8) wavelet.

Other choices are the Daublets D4 (shark fin), D6, and D8 and
The Haar wavelet (haar)

The program outputs:
d1 through d(n.levels), i.e. the n.level set of wavelet coefficients
s(n.levels), i.e. the scale coefficients associated with n.levels
long information concerning wavelet type (e.g. haar, D4,
etc.) along the attributes boundary and class which are
by default to dwt and periodic. For more information about
these attributes, see the waveslim documentation.

NOTES: plotts.dwt.wge plots a DWT based on the waveslim
function dwt (see the waveslim documentation for more details)

Example: To obtain the DWT shown in Figure 12.13a for the bumps256
data set, use the following commands:

```
data(bumps256)
plotts.dwt.wge(bumps256,n.levels = 5,type = 'D6')
```

+   plotts.mra(x,n.levels)
x is the realization to be analyzed (x must be a vector of length
length 2^j₀ for some positive integer j₀ between 2 and 14.
n.levels (default = 4) is the number of levels (n.levels ≤ j₀)
type specifies the type of wavelet used (default = S8), i.e.
Symlet(8) wavelet. Other choices are the Daubletlets D4
(shark fin), D6, and D8 and the Haar wavelet (haar).