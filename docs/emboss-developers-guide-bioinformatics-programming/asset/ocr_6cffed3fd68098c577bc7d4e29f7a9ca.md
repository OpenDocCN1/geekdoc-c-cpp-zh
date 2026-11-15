# 6.6.5 AJAX datatypes

The basic AJAX datatype for handling patterns is:

+   - AjPRegexp Regular expression

Two AJAX datatypes are provided for handling lists of patterns including input patterns defined in the ACD file. These are lists of individual patterns and regular expressions using the datatypes below.:

+   - AjPPatlistSeq Sequence pattern list object holding a list of sequence patterns and associated information (for pattern ACD datatype)
+   - AjPPatlistRegex General pattern list object holding a list of general patterns and associated information (for regexp ACD datatype)

The following AJAX datatypes are provided for handling regular expressions at a low level beyond that provided by the static data structures and functions. You are unlikely to need to use these directly:

+   - AjPPatComp All required data for compiling and searching
+   - AjPPatternSeq Definition of feature pattern
+   - AjPPatternRegex Holds definition of feature pattern

# 6.6.6 ACD file handling

Datatypes and functions for handling pattern input via the ACD file are shown below.

| Title | To read a regular expression | To read a sequence pattern |
| :--- | :--- | :--- |
| ACD datatype | regexp | pattern |
| AJAX datatype | AjPPatlistRegex | AjPPatlistSeq |
| To retrieve from ACD | ajAcdGetRegexp | ajAcdGetPattern |

Your application code will call embInit to process the ACD file and command line (see Section 6.3, ‘Handling ACD files’). All values from the ACD file are read into memory. You have a handle on memory through the ajAcdGet* family of functions which return pointers to appropriate objects.

# 6.6.6.1 Input pattern retrieval

To retrieve an input pattern an object pointer is declared and then initialised using the appropriate ajAcdGet* function.