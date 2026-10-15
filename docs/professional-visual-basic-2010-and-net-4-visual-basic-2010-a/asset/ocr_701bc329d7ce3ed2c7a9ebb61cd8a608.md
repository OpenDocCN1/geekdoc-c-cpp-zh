Add multiple namespaces by separating them with a comma:

```
`vbc.exe MyModule.vb /imports:System, System.Data`
```

# /langversion

This option enables you to specify a language version. This version is based on the Visual Basic version not the .NET version. For example, .NET 4 ships with Visual Basic 10.

```
`vbc.exe MyModule.vb /langversion:10`
```

# /optionexplicit[+:-]

Always a good idea, using /optionexplicit causes the compiler to check whether any variables in the code are used before they are even declared (yes, this is possible and very bad practice). Using this setting, when variables are found before they are even declared, the compiler throws an error. By default, the compiler does not check the code using the /optionexplicit option. Use this option as shown in the following example:

```
`vbc.exe MyModule.vb /optionexplicit`
```

# /optionstrict[+:-]

It’s also a good idea to use the /optionstrict option in the compilation process. Using this option causes the compiler to check whether you are making any improper type conversions in your code. Widening type conversions are allowed, but when you start performing narrowing type conversions, using this option will cause an error to be thrown by the compiler. By default, the compiler does not look for these types of errors with your type conversions. Use this option as follows:

```
`vbc.exe MyModule.vb /optionstrict`
```

# /optioncompare

By default, the Visual Basic compiler compares strings using a binary comparison. If you want the string comparisons to use a text comparison, then use the following construction:

```
`vbc.exe MyModule.vb /optioncompare:text`
```

# /optioninfer[+:-]

New to the .NET Framework 3.5 version of the compiler, this option specifies that you want to allow type inference of variables. Use this option as illustrated in the following example:

```
`vbc.exe MyModule.vb /optioninfer`
```

# /rootnamespace

Use this option to specify the namespace to use for compilation:

```
`vbc.exe MyClass.vb /rootnamespace:Reuters`
```

# Miscellaneous Features

The rest of this appendix covers some of the other very useful features in the compiler

# /?

When you don’t have this book for reference, you can use the Visual Basic compiler for a list of options by using the /? option, as shown here:

```
`vbc.exe /?`
```

This causes the entire list of options and their definitions to be displayed in the command window.