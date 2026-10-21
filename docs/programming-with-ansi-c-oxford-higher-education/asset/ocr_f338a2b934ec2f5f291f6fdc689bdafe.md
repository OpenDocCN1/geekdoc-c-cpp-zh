Thus, a solution similar to the non-inline functions for the templates is needed. It is possible using another model that uses the keyword export (discussed in the following section), where it is possible to define a template function at a single place and use declarations at other places.

# export Keyword

The keyword export is useful when a template function is defined at a single place and the declarations are used at other places. This is useful in instances where the templates defined while developing one application are found to be useful for other applications or when the templates designed by somebody else are to be used.

Suppose we define BubbleSort.cpp to contain the definition of the generic bubble sort. Then, it is possible to modify the definition as follows:

```
export template <typename Type>
void GenericBubbleSort(Type TempIntArray[])
{
    Body of the function
}
```

> Note In separate compilation model, the definition of the template definition is preceded by the keyword export in the file in which the templates are defined. In all other files, only the prototype of the template is specified.

If we want to use the same GenericBubbleSort() in UseIt.cpp, then the code in UseIt.cpp contains only the following:

```
{
    template <typename Type>
    void GenericBubbleSort(Type TempIntArray[]);
    /* Note the semicolon; it indicates the end */
    // No definition of the template
    // Other code
}
```

However, while linking UseIt.cpp, we just need to provide the .obj file of the BubbleSort program.

Note that in the earlier case the entire body of GenericBubbleSort() should be copied to UseIt.cpp.

The first model where template definitions are copied to all the files is called inclusion compilation model and the second one is known as separate compilation model as implementation is separated from the interface here.

# 7.5 USE OF typename

The keyword typename indicates that the expression following the keyword is the name of a type. We have used typename in the <> section in the template. It can also be used within the body of the template function (or template class function).

If we write a typename identifier, then that identifier is treated as a type in that function template as shown in Program 7.12.