# 10.6 PROCEDURAL CONSTRUCTS AND DEFMODULES

In a similar manner to deftemplate constructs, defglobal, deffunction, and defgeneric constructs can be imported and exported by modules. Four of the possible export and import statements discussed in Chapter 9 with relation to deftemplates apply the same behavior to the procedural constructs:

```
(export ?ALL)
(export ?NONE)
(import <module-name> ?ALL)
(import <module-name> ?NONE)
```

The first format will export all exportable constructs from a module; the second format indicates that no constructs are exported; the third format imports all exported constructs from the specified module; and the fourth format imports none of the exported constructs from the specified module.

Each of the defglobal, deffunction, and defgeneric constructs also has associated import/export statements that allow you to specify whether all, none, or a specified set of each construct should be imported/exported:

```
(export defglobal ?ALL)
(export defglobal ?NONE)
(export defglobal <defglobal-name>+)
```

```
(export deffunction ?ALL)
(export deffunction ?NONE)
(export deffunction <deffunction-name>+)
```

```
(export defgeneric ?ALL)
(export defgeneric ?NONE)
(export defgeneric <defgeneric-name>+)
```

```
(import <module-name> defglobal ?ALL)
(import <module-name> defglobal ?NONE)
(import <module-name> defglobal <defglobal-name>+)
```

```
(import <module-name> deffunction ?ALL)
(import <module-name> deffunction ?NONE)
(import <module-name> deffunction <deffunction-name>+)
```

```
(import <module-name> defgeneric ?ALL)
(import <module-name> defgeneric ?NONE)
(import <module-name> defgeneric <defgeneric-name>+)
```