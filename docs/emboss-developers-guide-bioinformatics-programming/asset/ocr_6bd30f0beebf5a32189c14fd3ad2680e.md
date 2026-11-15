other AJO* datatypes) are never used in EMBOSS. Instead, memory for an instance of the object in memory is dynamically allocated to the pointer AjPStr (see Section 5.5, ‘Programming with objects’). For this reason, AjPStr is given after “Name” in SRS and for the sake of brevity, “object” is often used to refer to an AjPStr (for example) when what is really meant is “object pointer”. The use of objects and pointers is covered in depth elsewhere (Section 5.5, ‘Programming with objects’).

EDATA and EDATAREL include links to functions that use each object, which is handy if you want to know what you can do with an object. The functions in EFUNC and EFUNCREL are organised into categories of related functionality that correspond to sections in the C source file (see Appendix D, Code documentation standards and below).

After the Alias(es) section you’ll see several more blocks functions within a category. The categories you see will depend upon the library file, but might include:

+   Iterators – iteration, e.g. over individual characters in a string.
+   Constructors – create new instances of an object (allocate memory).
+   Destructors – destroy instances of an object (free memory).
+   Assignments – initialise an object, replace contents if necessary.
+   Modifiers – change or replace the contents of an object.
+   Operators – use, but do not change, the contents of an object.
+   Outputs – write the contents of an object to an external file.
+   Casts – convert an object into an object or data of another type.

At the bottom of the page you’ll see the following section:

+   Attributes lists the elements of the C data structure.
+   Body gives the C code for the object definition.

# 1.3.4.1.2 Searching EFUNC

The EFUNC database can be searched directly. This is useful if you know the kind of function you want but don’t know the name. The function names and names and order of function parameters have been standardised (see Section D.1, ‘Code documentation standards’) to be intuitive and consistent.

Let’s assume you want to search for a function that appends one string to another:

+   1. Return to the SRS databases page, uncheck the EDATA database and check the check-box for the EFUNC database.
+   2. Select the query form.
+   3. It’s often best to limit the search to the description field so as to retrieve more specific matches. So: change AllText to Description.
+   4. Type append & string into the associated box, then click on Search.

A list of functions will appear. You can only use those functions that begin with aj or emb, public functions in the AJAX and NUCLEUS libraries respectively. The others are hidden functions, accessed by the internals of EMBOSS and not for general use.