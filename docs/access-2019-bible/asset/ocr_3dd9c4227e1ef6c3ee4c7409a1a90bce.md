The sResult variable will contain the String The quick brown fox jumped. Each element of the array is concatenated together with the delimiter inserted between them, in this case a single space.

# Understanding Subs and Functions

The code in a VBA application lives in containers called modules. As you learned in Chapter 24, modules exist behind the forms and reports in an Access application, as well as in stand-alone modules. The modules themselves contain many procedures, variable and constant declarations, and other directives to the VBA engine.

The code within the modules is composed of procedures. There are two main types of procedures in VBA: subroutines or subprocedures (often called subs) and functions.

The general rules for procedures include the following:

+   You must give the procedure a unique name within its scope (see “Understanding variable scope and lifetime,” earlier in this chapter). Although it isn’t a good idea—because of the chance of confusing the VBA engine or another person working with your code—it is possible to have more than one procedure with the same name, as long as the name is unique within each procedure’s scope.

+   The name you assign to a procedure can’t be the same as a VBA keyword.

+   A procedure and a module cannot have the same name. This is one place where a naming convention can be very useful. If you always prefix module names with bas or mod, you don’t run the risk of an error occurring from having a procedure and module with the same name.

+   A procedure can’t contain other procedures within it. A procedure can, however, call another procedure and execute the code in the other procedure at any time.

Because of the rules governing procedure scope, you can’t have two public procedures both named MyProcedure, although you can have two private procedures, both named MyProcedure, or one public procedure named MyProcedure and one private procedure named MyProcedure, but not in the same module. The reason it’s a bad idea to use the same procedure name for multiple procedures, even when the procedures have different scopes, should be obvious.

The following sections cover some of the specifics regarding VBA procedures. Planning and composing the procedures in your modules is the most time-consuming part of working with VBA, so it’s important to understand how procedures fit into the overall scheme of application development.

Subroutines and functions both contain lines of code that you can run. When you run a subroutine or function, you call it. Calling, running, and invoking are all terms meaning to execute (or run) the statements (or lines of code) within the procedure or function. All