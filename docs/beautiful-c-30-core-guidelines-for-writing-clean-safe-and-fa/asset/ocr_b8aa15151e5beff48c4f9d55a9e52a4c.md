Finally, we would observe that if you find yourself passing multiple in-out parameters to a function, there is a good chance that you are missing an abstraction. You may be attempting a kind of double (or more) dispatch and trying to confect a way of modeling the interactions of multiple classes. Be assured, this is not the place to do that.

# Summary

Advice from earlier times to arrange parameters in the order in, in-out, out is obviated by advances in C++.

+   - Mandatory copy elision for returning prvalues means that careful design of the constructor API can facilitate optimal return-by-value.
+   - Multiple values should be returned as a struct or as a tuple.
+   - Structured binding is preferable to tie as it is a language facility rather than a library facility. Additionally, it obviates the need to default-construct the object you’re going to tie to the return value.
+   - In-out parameters can individually expand the API of a class and should be placed before the input parameters.
+   - Returning in-out parameters can be used to daisy-chain function calls in the style of the chevron operator, although effort is required to make this legible.
+   - Multiple in-out parameters require special care and may hint at a missing abstraction.