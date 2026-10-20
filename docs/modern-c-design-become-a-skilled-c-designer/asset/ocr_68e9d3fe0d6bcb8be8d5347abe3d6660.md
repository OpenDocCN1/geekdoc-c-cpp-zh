# A Quick Note on Actual Implementation

For the purposes of this text, the interfaces developed, as exemplified by Table 2-2, represent idealizations of the actual interfaces deployed in the code. The actual code may differ somewhat in the syntax, but the semantic intent of the interface will always be preserved. For example, in Table 2-2, we have defined the interface to get n elements as void getElements(n, vector<double>&), which is a perfectly serviceable interface. However, using new features of modern C++ (see the sidebar on move semantics),

the implementation makes use of rvalue references and move construction by also providing vector<double> getElements(n) as a logically equivalent, overloaded interface.

Defining good C++ interfaces is a highly nontrivial task; I know of at least one excellent book dedicated entirely to this subject [20]. Here in this book, I only provide a sufficient level of detail about the interfaces