Turning off the CS1591 warning, for example, would appear on the com-mand line as shown in Output 4.30.

# **OUTPUT 4.30**

```
`> csc /doc:generate.xml /nowarn:1591 /out:generate.exe Program.cs`
```

# ### Specifying Line Numbers (#line)

The #line directive controls on which line number the C# compiler reports an error or warning. It is used predominantly by utilities and designers that emit C# code. In Listing 4.61, the actual line numbers within the file appear on the left.

# **LISTING 4.61: The #line Preprocessor Directive**

```
```
124  #line 113 "TicTacToe.cs"
125  #warning "Same move allowed multiple times."
126  #line default
```
```

Including the #line directive causes the compiler to report the warning found on line 125 as though it were on line 113, as shown in the compiler error message in Output 4.31.

# **OUTPUT 4.31**

```
```
Performing main compilation...
...TicTacToe.cs(113,18): warning CS1030: #warning: "Same move allowed
multiple times."

Build complete -- 0 errors, 1 warnings
```
```

Following the #line directive with default reverses the effect of all prior #line directives and instructs the compiler to report true line numbers rather than the ones designated by previous uses of the #line directive.

# ### Hints for Visual Editors (#region, #endregion)

C# contains two preprocessor directives, #region and #endregion, that are useful only within the context of visual code editors. Code editors,