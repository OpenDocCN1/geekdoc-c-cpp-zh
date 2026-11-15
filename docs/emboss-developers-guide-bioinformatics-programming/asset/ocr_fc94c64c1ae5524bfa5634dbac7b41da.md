The application could be invoked in either of the following ways:

```
seqdemo filename.seq filename.out -abool
seqdemo filename.seq filename.out -noabool
```

In the first example the boolean qualifier abool is set to True. In fact, the value needn't have been set explicitly since the default value is True. In the second command line abool is set to False using the prefix no.

# 4.5.8.1 Prompting for boolean values

Care should be taken over the definition of the information: and help: global attributes for boolean datatypes. These are used to prompt the user (interactively or via a GUI) and to provide help text. The text provided in each case should reflect the expected default value of the boolean option, which may be the opposite of what the name implies. For example, if set to “Y” by default, then the command line option would typically be -noFlag where Flag is the qualifier. If set to “N” by default, then the default action may be the opposite of what the information or help text implies. If the value is calculated then the user may need some extra guidance.

# 4.6 ACD utilities

# 4.6.1 Introduction

EMBOSS includes six utilities that are used to run, test and document an ACD file without the need to write the C source code for the program itself:

+   **acdc** Reads and processes an ACD file, prompting the user as necessary in exactly the same way as if the application was running. If it encounters an error it will terminate. This allows the behaviour of the command line interface to be tested under different conditions, even if the application itself has not yet been written. It is the most widely used utility and is the basic tool for testing that an ACD file works correctly.

+   **acdtrace** Works the same as **acdc** but reports the processing of lines in an ACD file. It also prints the results of evaluating any variables and operations (see Section 4.4, ‘Operations’).

+   **acdvalid** Processes an ACD file and reports any errors or warnings caused by incorrect, deprecated or obsolete syntax. The tests go above and beyond those of **acdc** and **acdtrace**. It enforces recommendations for parameter and qualifier naming, and highlights ACD syntax that might cause problems to third-party parsing software.

+   **acdlog** Processes an ACD file and user input while logging the contents of internal data structures. For the time being its use is deprecated and the **entrails** application (see below) should be used instead.

+   **acdpretty** Generates a correctly formatted ACD file from one which is parsable but which is partly or incorrectly formatted.

+   **acdtable** Creates the table of parameters, allowed values and defaults, used in the application documentation and to provide user help.