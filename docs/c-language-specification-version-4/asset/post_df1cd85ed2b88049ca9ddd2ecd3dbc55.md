
otherwise processed. Within a conditional-section that is being processed as a skipped-section, any nested conditional-sections (contained in nested #if...#endif and #region...#endregion constructs) are also processed as skipped-sections.

The following example illustrates how conditional compilation directives can nest:

```
#define Debug    // Debugging on
#undef Trace    // Tracing off
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #if Trace
        writeToLog(this.ToString());
        #endif
        #endif
        CommitHelper();
    }
}
```

Except for pre-processing directives, skipped source code is not subject to lexical analysis. For example, the following is valid despite the unterminated comment in the #else section:

```
#define Debug    // Debugging on
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #else
        /* Do something else
        #endif
    }
}
```

Note, however, that pre-processing directives are required to be lexically correct even in skipped sections of source code.

Pre-processing directives are not processed when they appear inside multi-line input elements. For example, the program:

```
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello,
#if Debug
world
#else
Nebraska
#endif
");
    }
}
```

results in the output:

```
hello,
#if Debug
world
#else
Nebraska
#endif
```

In peculiar cases, the set of pre-processing directives that is processed might depend on the evaluation of the pp-expression. The example:

```
#if X
/*
#else
/* */ class Q { }
#endif
```

always produces the same token stream (class Q {}), regardless of whether or not X is defined. If X is defined, the only processed directives are #if and #endif, due to the multi-line comment. If X is undefined, then three directives (#if, #else, #endif) are part of the directive set.

### 2.5.5 Diagnostic directives

The diagnostic directives are used to explicitly generate error and warning messages that are reported in the same way as other compile-time errors and warnings.

```
pp-diagnostic:
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message

pp-message:
    new-line
    whitespace input-characters_opt new-line
```

The example:

```
#warning Code review needed before check-in
#if Debug && Retail
#error A build can't be both debug and retail
#endif
class Test {...}
```

always produces a warning ("Code review needed before check-in"), and produces a compile-time error ("A build can't be both debug and retail") if the conditional symbols Debug and Retail are both defined. Note that a pp-message can contain arbitrary text; specifically, it need not contain well-formed tokens, as shown by the single quote in the word can't.

### 2.5.6 Region directives

The region directives are used to explicitly mark regions of source code.

```
pp-region:
    pp-start-region conditional-section_opt pp-end-region
pp-start-region:
    whitespace_opt # whitespace_opt region pp-message
pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

No semantic meaning is attached to a region; regions are intended for use by the programmer or by automated tools to mark a section of source code. The message specified in a #region or #endregion directive likewise has no semantic meaning; it merely serves to identify the region. Matching #region and #endregion directives may have different pp-messages.

The lexical processing of a region:

```
#region
...
#endregion
```

corresponds exactly to the lexical processing of a conditional compilation directive of the form:

```
#if true
...
#endif
```

### 2.5.7 Line directives

Line directives may be used to alter the line numbers and source file names that are reported by the compiler in output such as warnings and errors.

Line directives are most commonly used in meta-programming tools that generate C# source code from some other text input.

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
file-name:
    " file-name-characters "
file-name-characters:
    file-name-character
    file-name-characters file-name-character
file-name-character:
    Any input-character except "
```

When no #line directives are present, the compiler reports true line numbers and source file names in its output. When processing a #line directive that includes a line-indicator that is not default, the compiler treats the line after the directive as having the given line number (and file name, if specified).

A #line default directive reverses the effect of all preceding #line directives. The compiler reports true line information for subsequent lines, precisely as if no #line directives had been processed.

A #line hidden directive has no effect on the file and line numbers reported in error messages, but does affect source level debugging. When debugging, all lines between a #line hidden directive and the subsequent #line directive (that is not #line hidden) have no line number information. When stepping through code in the debugger, these lines will be skipped entirely.

Note that a file-name differs from a regular string literal in that escape characters are not processed; the '\' character simply designates an ordinary backslash character within a file-name.

### 2.5.8 Pragma directives

The #pragma preprocessing directive is used to specify optional contextual information to the compiler. The information supplied in a #pragma directive will never change program semantics.

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
pragma-body:
    pragma-warning-body
```

C# provides #pragma directives to control compiler warnings. Future versions of the language may include additional #pragma directives. To ensure interoperability with other C# compilers, the Microsoft C# compiler
does not issue compilation errors for unknown #pragma directives; such directives do however generate warnings.

### 2.5.8.1 Pragma warning

The #pragma warning directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
warning-action:
    disable
    restore
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
```

A #pragma warning directive that omits the warning list affects all warnings. A #pragma warning directive that includes a warning list affects only those warnings that are specified in the list.

A #pragma warning disable directive disables all or the given set of warnings.

A #pragma warning restore directive restores all or the given set of warnings to the state that was in effect at the beginning of the compilation unit. Note that if a particular warning was disabled externally, a #pragma warning restore (whether for all or the specific warning) will not re-enable that warning.

The following example shows use of #pragma warning to temporarily disable the warning reported when obsolete members are referenced, using the warning number from the Microsoft C# compiler.

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

## 3. Basic concepts

### 3.1 Application Startup

An assembly that has an entry point is called an application. When an application is run, a new application domain is created. Several different instantiations of an application may exist on the same machine at the same time, and each has its own application domain.

An application domain enables application isolation by acting as a container for application state. An application domain acts as a container and boundary for the types defined in the application and the class libraries it uses. Types loaded into one application domain are distinct from the same type loaded into another application domain, and instances of objects are not directly shared between application domains. For instance, each application domain has its own copy of static variables for these types, and a static constructor for a type is run at most once per application domain. Implementations are free to provide implementation-specific policy or mechanisms for the creation and destruction of application domains.

Application startup occurs when the execution environment calls a designated method, which is referred to as the application's entry point. This entry point method is always named Main, and can have one of the following signatures:

```
static void Main() {...}
static void Main(string[] args) {...}
static int Main() {...}
static int Main(string[] args) {...}
```

As shown, the entry point may optionally return an int value. This return value is used in application termination (§3.2)

The entry point may optionally have one formal parameter. The parameter may have any name, but the type of the parameter must be string[]. If the formal parameter is present, the execution environment creates and passes a string[] argument containing the command-line arguments that were specified when the application was started. The string[] argument is never null, but it may have a length of zero if no command-line arguments were specified.

Since C# supports method overloading, a class or struct may contain multiple definitions of some method, provided each has a different signature. However, within a single program, no class or struct may contain more than one method called Main whose definition qualifies it to be used as an application entry point. Other overloaded versions of Main are permitted, however, provided they have more than one parameter, or their only parameter is other than type string[].

An application can be made up of multiple classes or structs. It is possible for more than one of these classes or structs to contain a method called Main whose definition qualifies it to be used as an application entry point. In such cases, an external mechanism (such as a command-line compiler option) must be used to select one of these Main methods as the entry point.

In C#, every method must be defined as a member of a class or struct. Ordinarily, the declared accessibility (§3.5.1) of a method is determined by the access modifiers (§10.3.5) specified in its declaration, and similarly the declared accessibility of a type is determined by the access modifiers specified in its declaration. In order for a given method of a given type to be callable, both the type and the member must be accessible. However, the application entry point is a special case. Specifically, the execution environment can access the application's
