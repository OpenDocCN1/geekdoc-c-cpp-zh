# FIGURE 25.2

Declaring a public variable.

![](bbox=[0.2, 0.26, 0.6, 0.47])

# CAUTION

You cannot declare a public variable within a procedure. It must be declared in the declarations section of a module. If you try to declare a variable public within a procedure, you get an error message.

Although you can declare a public variable in any module, the best practice for declaring public variables is to declare them all in a single standard module that's used only to store public variables. Public variables, while necessary in some cases, should be limited. Because any procedure in your project can change a public variable's value, it can be difficult to find which procedure is making an unwanted change. With all the publically declared variables in one place, it's easy to locate them, and it's easy to see if you're using too many and may need to rethink your code structure.

# Tip

You can declare public variables in the code module attached to a form or report. Referencing these public variables from another module is a little bit different than referencing public variables declared in standard modules. To reference the value of a public variable declared behind a form or report from another module, you must qualify the variable reference, using the name of the form or report object. frmMainForm.MyVariable, for example, accesses a form named frmMainForm and obtains the value of the public variable MyVariable declared in the form's code module. Public variables declared within a form or report's module cannot be referenced unless the form or report is open.

# The Private keyword

The declarations section in Figure 25.2 shows the use of the Private keyword to declare variables. Technically, there is no difference between Private and Dim when used in the declarations section of a module, but using Private at the module level to declare variables that are available to only that module's procedures is a good idea. The Private