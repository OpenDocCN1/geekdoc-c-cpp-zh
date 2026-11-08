# ## 2.1 Global declarations

Unlike the other sections the global declaration section itself is a sequence of subsections declaring different objects to be used throughout the remainder of the program. Fig. 2 gives an overview and defines the exact syntax.

![](bbox=[0.181, 0.177, 0.848, 0.389])

Fig. 2. CAOS global declaration syntax

The first set of declarations refers to types. CAOS is not a particularly versatile language when it comes to types and type constructors. We deliberately restrict ourselves here; extending the language design by additional machine-supported basic types and standard type constructors like records is merely a matter of engineering, not of language design. In essence, CAOS supports three built-in types: Boolean values (`bool`), machine word integer numbers (`int`) and double precision floating point numbers (`double`). The only type constructor CAOS supports for now is symbolic enumeration types as known from C. We do advocate a symbolic style of programming in contrast to a machine-oriented one. Taking Conway’s famous Game of Life as a running example, we would suggest to define an enumeration type `dead_or_alive` rather than encoding these different states in Boolean or integer values

The `const` keyword marks the second kind of global declarations; it is used to declare an identifier with a compile time constant value. Again we recommend to define symbolic constants for relevant numerical values to improve the readability of code.

In addition to (compile time) constants CAOS also features simulation *parameters*. These are compile time symbolic values, but runtime constants initialised during program startup. Parameters are declared using the `param` keyword. Like a constant a parameter has a type, a name and a (default) value. The difference is that the given value indeed only is a default value. This default value may be overwritten upon startup of a simulation through a command line parameter. Parameters are a very useful feature if a simulation needs to be run several times for different parameter sets, e.g. from a shell script. Typical applications for parameters are the initialization of

+   - values of cell components,
+   - used variables in the cell behavior,
+   - time steps for observations,

but many others are possible. The keyword `param` may be followed by an optional string enclosed in quotation marks to compile a short description of the parameter into the executable. The information given here will be displayed within the help text that a compiled CAOS program displays if `--help` is passed as command line parameter.

It is possible to use external functions in a CAOS program via the `extern` keyword and a C-style function prototype. The main intended use of this feature is to make mathematical