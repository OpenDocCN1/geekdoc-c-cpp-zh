with the default being:

+   - Advanced qualifier

The attributes to use are as follows:

```
parameter:  "Y"
standard:   "Y"
additional: "Y"
```

parameter: "Y" means that the data definition is a _parameter_. standard: "Y" and additional: "Y" mean that the data definition is a _standard qualifier_ or an _additional qualifier_. If none of parameter: "Y", standard: "Y" or additional: "Y" are specified then the data definition defaults to being an _advanced qualifier_. Parameters are commonly used for input and output files and other primary input and output data, whereas the different types of qualifier are used for other application options.

> **Caution**
> 
> Only one of parameter: "Y", standard: "Y" or additional: "Y" should ever be given in a data definition. If more than one is used an error message will be generated during ACD processing.

> **Note**
> 
> You should never explicitly specify Parameter: "N", standard: "N" or additional: "N". An error will be generated during ACD processing if you do. In practice, calculated values of “N” are in fact supported and can be used, in exceptional circumstances, to override the default behaviour of these attributes (see Section 4.5, ‘Controlling the prompt’).

> **Note**
> 
> In earlier versions of EMBOSS, required: and optional: were used.
> 
> standard: now replaces required: and additional: replaces optional:.

The difference between parameters and qualifiers is that you don’t have to use a flag to specify a value for a parameter on the command line. Values are specified like this:

```
_ApplicationName Option Value._
```