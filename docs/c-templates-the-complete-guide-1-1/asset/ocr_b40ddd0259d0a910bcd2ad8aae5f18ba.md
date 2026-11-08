predefined constructors or assignment operators.

+   - By using braced initialization or explicitly calling a default constructor, you can ensure that variables and members of templates are initialized with a default value even if they are instantiated with a built-in type.
+   - You can provide specific templates for raw arrays, which can also be applicable to string literals.
+   - When passing raw arrays or string literals, arguments decay (perform an array-to-pointer conversion) during argument deduction if and only if the parameter is not a reference.
+   - You can define variable templates (since C++14).
+   - You can also use class templates as template parameters, as template template parameters.
+   - Template template arguments must usually match their parameters exactly.

+   1. That is, in a constructor with a parameter of type std::initializer_list, for some type T.
+   2. Parameters of type T[4] - for some arbitrary type T - have to be valid only in C++17, though the resolution of Core issue 1657, however, many compilers accepted such parameters in earlier versions of the language.
+   3. This is a basic implementation to demonstrate the template features, hence the proper exception handling are currently missing.
+   4. Yes, you have very similar terms for very different things. A variable template is a template that is a template (variable is an array here?). A variable template is a template for a variable, number of template parameters (variables is an arbitrary here).
+   5. Before C++17, there is an issue with this version that we explain in a minute. However, that affects only the default value std::integer. Thus, we can illustrate the general features of template template parameters with this default value before we discuss how to deal with it before C++17.