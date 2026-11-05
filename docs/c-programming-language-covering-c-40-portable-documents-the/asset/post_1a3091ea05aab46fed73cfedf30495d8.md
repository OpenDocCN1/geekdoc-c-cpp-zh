
## 2.5.7 Line Directives

Line directives may be used to alter the line numbers and source file names that are reported by the compiler in output such as warnings and errors.

Line directives are most commonly used in meta-programming tools that generate C# source code from some other text input.

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
```

```
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
```

```
file-name:
    " file-name-characters "
```

```
file-name-characters:
    file-name-character
    file-name-characters file-name-character
```

```
file-name-character:
    Any input-character except "
```

When no #line directives are present, the compiler reports true line numbers and source file names in its output. When processing a #line directive that includes a line-indicator that is not default, the compiler treats the line after the directive as having the given line number (and file name, if specified).

> **JON SKEET** If you're writing a tool that generates code from some other source, you might think that the easiest approach is to just include a #line directive for every line you output. It's not quite that simple, however: A #line directive within a verbatim string literal ends up as part of the string, rather than being treated as a directive. So the following code almost certainly doesn't work as intended:
>
> ```
> #line 5
> Console.WriteLine(@"First line
> #line 6
> Second line");
> ```

A #line default directive reverses the effect of all preceding #line directives. The compiler reports true line information for subsequent lines, precisely as if no #line directives had been processed.

A #line hidden directive has no effect on the file and line numbers reported in error messages, but does affect source-level debugging. When debugging, all lines between a #line hidden directive and the subsequent #line directive (that is not #line hidden) have no line number information. When stepping through code in the debugger, these lines will be skipped entirely.

Note that a file-name differs from a regular string literal in that escape characters are not processed; the `\` character simply designates an ordinary backslash character within a file-name.

## 2.5.8 Pragma Directives

The #pragma preprocessing directive is used to specify optional contextual information to the compiler. The information supplied in a #pragma directive will never change program semantics.

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line

pragma-body:
    pragma-warning-body
```

C# provides #pragma directives to control compiler warnings. Future versions of the language may include additional #pragma directives. To ensure interoperability with other C# compilers, the Microsoft C# compiler does not issue compilation errors for unknown #pragma directives; such directives do, however, generate warnings.

### 2.5.8.1 Pragma Warning

The #pragma warning directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list

warning-action:
    disable
    restore
```

```
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
```

A #pragma warning directive that omits the warning list affects all warnings. A #pragma warning directive that includes a warning list affects only those warnings that are specified in the list.

> **JON SKEET** I'm not sure that defaulting to affecting all warnings is a good idea. Requiring an explicit "all" as an alternative warning list wouldn't have conflicted with any other warnings (because individual warnings have to be numeric) and it would make the meaning a good deal clearer. Having said this, I've never seen anyone disable all warnings—and I hope never to do so.

A #pragma warning disable directive disables all or the given set of warnings.

A #pragma warning restore directive restores all or the given set of warnings to the state that was in effect at the beginning of the compilation unit. Note that if a particular warning was disabled externally, a #pragma warning restore (whether for all or the specific warning) will not re-enable that warning.

The following example shows use of #pragma warning to temporarily disable the warning reported when obsoleted members are referenced, using the warning number from the Microsoft C# compiler.

```
using System;
class Program
{
    [Obsolete]
    static void Foo() {}
    static void Main() {
        #pragma warning disable 612
        Foo();
        #pragma warning restore 612
    }
}
```

> **JOSEPH ALBAHARI** The compiler generates a warning when it detects a condition that might possibly indicate a mistake in the code. Because of the potential for false positives, the ability to disable certain warnings over selected lines of code is important in maintaining a good signal-to-noise ratio—so that the real mistakes are noticed. It's also essential if you want to instruct the compiler to treat warnings as errors—something I do in my own projects.

## 3. Basic Concepts

### 3.1 Application Start-up

An assembly that has an entry point is called an application. When an application is run, a new application domain is created. Several different instantiations of an application may exist on the same machine at the same time, and each has its own application domain.

An application domain enables application isolation by acting as a container for application state. An application domain acts as a container and boundary for the types defined in the application and the class libraries it uses. Types loaded into one application domain are distinct from the same type loaded into another application domain, and instances of objects are not directly shared between application domains. For instance, each application domain has its own copy of static variables for these types, and a static constructor for a type is run at most once per application domain. Implementations are free to provide implementation-specific policy or mechanisms for the creation and destruction of application domains.

*Application start-up* occurs when the execution environment calls a designated method, which is referred to as the application's entry point. This entry point method is always named Main, and can have one of the following signatures:

```
static void Main() { ... }
static void Main(string[] args) { ... }
static int Main() { ... }
static int Main(string[] args) { ... }
```

As shown, the entry point may optionally return an int value. This return value is used in application termination (§3.2).

The entry point may optionally have one formal parameter. The parameter may have any name, but the type of the parameter must be string[]. If the formal parameter is present, the execution environment creates and passes a string[] argument containing the command-line arguments that were specified when the application was started. The string[] argument is never null, but it may have a length of zero if no command-line arguments were specified.

Since C# supports method overloading, a class or struct may contain multiple definitions of some method, provided each has a different signature. However, within a single program, no class or struct may contain more than one method called `Main` whose definition qualifies it to be used as an application entry point. Other overloaded versions of `Main` are permitted, however, provided they have more than one parameter, or their only parameter is other than `type string[]`.

An application can be made up of multiple classes or structs. It is possible for more than one of these classes or structs to contain a method called `Main` whose definition qualifies it to be used as an application entry point. In such cases, an external mechanism (such as a command-line compiler option) must be used to select one of these `Main` methods as the entry point.

> **ERIC LIPPERT**: The "csc" command-line compiler provides the /main: switch for this purpose.

In C#, every method must be defined as a member of a class or struct. Ordinarily, the declared accessibility (§3.5.1) of a method is determined by the access modifiers (§10.3.5) specified in its declaration, and similarly the declared accessibility of a type is determined by the access modifiers specified in its declaration. For a given method of a given type to be callable, both the type and the member must be accessible. However, the application entry point is a special case. Specifically, the execution environment can access the application's entry point regardless of its declared accessibility and regardless of the declared accessibility of its enclosing type declarations.

The application entry point method may not be in a generic class declaration.

In all other respects, entry point methods behave like those that are not entry points.

### 3.2 Application Termination

*Application termination* returns control to the execution environment.

If the return type of the application's *entry point* method is `int`, the value returned serves as the application's *termination status code*. The purpose of this code is to allow communication of success or failure to the execution environment.

If the return type of the entry point method is `void`, reaching the right brace (`}`) that terminates the method, or executing a `return` statement that has no expression, results in a termination status code of `0`.
