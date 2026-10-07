
# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

## 5. Environment

An implementation translates C source files and executes C programs in two data-processing-system environments, which will be called the translation environment and the execution environment in this International Standard. Their characteristics define and constrain the results of conforming C programs constructed according to the syntactic and semantic rules for conforming implementations.

Forward references: In this clause, only a few of many possible forward references have been noted.

## 5.1 Conceptual models

### 5.1.1 Translation environment

#### 5.1.1.1 Translation structure

A program need not be translated at the same time. The text of the program is kept in units called source (or preprocessing files) in this International Standard. A source file together with all the headers and source files included via the preprocessing directive #include is known as a preprocessing unit. After preprocessing, a preprocessing translation unit is called a translation unit. Previously translated units may be preserved independently or in libraries. The separate translation units of a program communicate (for example) calls to functions whose identifiers have external linkage, manipulation of objects whose identifiers have external linkage, or manipulation of data files. Translation units may be separately translated and then later linked to produce an executable program.

Forward references: linkages of identifiers (6.2.2), external definitions (6.9), preprocessing directives (6.10).

### 5.1.1.2 Translation phases

The precedence among the syntax rules of translation is specified by the following phases⁶

- 1. Physical source file multibyte characters are mapped, in an implementation-defined manner, to the source file (introducing new-line characters for end-of-line indicators) if necessary. Trigraph sequences are replaced by corresponding single-character internal representations.

> 6 Implementations shall behave as if these separate phases occur, even though many are folded together in practice. Source files, translations, and translated units need not necessarily be stored as files, nor need there be any one-to-one correspondence between these entities and an external representation. The description is conceptual only, and does not specify any

- 2. Each instance of a backslash character (\) immediately followed by a new-line character is deleted, splicing physical source lines to form logical source lines. Only the last backslash on any physical source line shall be eligible for being part of such splice. A source file that is not empty shall contain a new-line character, which shall not be immediately preceded by a backslash character before any splicing taking place.

- 3. The source file is decomposed into preprocessing tokens^7) and sequences of white-space characters (including comments). A source file does not end in a partial preprocessing token or in a partial comment is replaced by one space character. New-line characters are retained. Whether a nonempty sequence of white-space characters other than new-line is retained or replaced by one space character is implementation-defined.

- 4. Preprocessing directives are executed, macro invocations are expanded, and #pragma. If a sequence that matches the syntax of a universal character name is produced by token concatenation (6.10.3), the behavior is undefined. A #include preprocessing directive causes the named header or source file to be processed from phase 1 through phase 4, recursively. All preprocessing directives are deleted.

- 5. Each source character set member and escape sequence in character constants and string literals is converted to the corresponding member of the execution character set; if there is no corresponding member, it is converted to an implementation-defined member other than the null (wide) character.^8

- 6. Adjacent string literal tokens are concatenated.

- 7. White-space characters separating tokens are no longer significant. Each preprocessing token is converted into a token. The resulting tokens are syntactically and semantically analyzed and translated as a translation unit.

- 8. All external object and function references are referenced. Library components are linked to satisfy references to functions and objects not defined in the current translation. All such translator output is collected into a program image which contains information needed for execution in its execution environment.

**Forward references:** universal character names (6.4.3), lexical elements (6.4), preprocessing directives (6.10), trigraph sequences (5.2.1.1), external definitions (6.9).

^7) As described in 6.4, the process of dividing a source file's characters into preprocessing tokens is context-dependent. For example, see the handling of < within a #include preprocessing directive.

^8) An implementation will not convert all non-corresponding source characters to the same execution character.

### 5.1.1.3 Diagnostics

A conforming implementation shall produce at least one diagnostic message (identified in an implementation-defined manner) if a pretranslation unit or translation unit contains a violation of any syntax rule or constraint, even if the behavior is explicitly specified as undefined or implementation-defined. Diagnostic messages need not be produced in other circumstances.⁹

EXAMPLE An implementation is required to issue a diagnostic for the translation unit:

```
char i;
int i;
```

because in those cases where wording in this International Standard describes the behavior for a construct as both a constraint error and resulting in undefined behavior, the constraint error shall be diagnosed.

## 5.1.2 Execution environments

Two execution environments are defined: freestanding and hosted. In both cases, program startup occurs when a designated C function is called by the execution environment. All objects with storage duration must be initialized (set to their initial values) before program startup. The manner and timing of such initialization are otherwise unspecified. Program termination returns control to the execution environment.

Forward references: storage durations of objects (6.2.4), initialization (6.7.9).

### 5.1.2.1 Freestanding environment

In a freestanding environment (where C program execution take place without benefit of an operating system), the name and type of the function called at program startup are implementation-defined. Any library facilities available to a freestanding program, other than the minimal set required by clause 4, are implementation-defined.

The effect of program termination in a freestanding environment is implementation-defined.

### 5.1.2.2 Hosted environment

A hosted environment need not be provided, but shall conform to the following specifications if present.

> ⁹ The intent is that an implementation should identify the nature of, and where possible localize, each violation. Of course, an implementation is free to produce any number of diagnostics as long as a valid program is still correctly translated. It may also successfully translate an invalid program.

#### 5.1.2.2.1 Program startup

The function called at startup is named main. The implementation declares no prototype for this function. It shall be defined with a return type of int and with no parameters:

```
int main(void) { /* ... */ }
```

or with two parameters (referred to here as argc and argv) though any names may be used, as they are local to the function in which they are declared:

```
int main(int argc, char *argv[]) { /* ... */ }
```
or equivalent;^10 or in some other implementation-defined manner.

If they are declared, the parameters to the main function shall obey the following constraints:

- The value of argc shall be nonnegative.
- argv[argc] shall be a null pointer.
- If the value of argc is greater than zero, the array members argv[0] through argv[argc-1] inclusive shall contain pointers to strings, which are given implementation-defined values by the host environment prior to program startup. The intent is to supply the program information determined prior to program startup from elsewhere in the hosted environment. If the host environment is not capable of supplying strings with both uppercase and lowercase, the implementation shall ensure that the strings are received in lowercase.
- If the value of argc is greater than zero, the string pointed to by argv[0] represents the program name; argv[0] shall be the null character if the program name is not available from the host environment. If the value of argc is greater than one, the strings pointed to by argv[1] through argv[argc-1] represent the program parameters.
- The parameters argc and argv and the strings pointed to by the argv array shall be modifiable by the program, and retain their last-stored values between program startup and termination.

#### 5.1.2.2.2 Program execution

In a hosted environment, a program may use all the functions, macros, type definitions, and objects described in the library clause (clause 7).

^10 Thus, int can be replaced by a typedef named as int, or the type of argv can be written as char **argv, and so on.
