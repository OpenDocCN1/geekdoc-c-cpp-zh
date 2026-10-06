case, we can simply put quotes around the file name.

When compiling a project on different platforms, it might be necessary to specify different files or different options based on the platform. The general syntax for conditionals in qmake

```
condition {
  then-case
} else {
  else-case
}
```

The condition part can be a platform name (e.g., win32, unix, or macx) or a more complex predicate. The then-case and else-case parts specify the values of variables using the standard syntax. For example:

```
win32 {
  SOURCES += serial_win.cpp
} else {
  SOURCES += serial_unix.cpp
}
```

The else branch is optional. For convenience, qmake also supports a one-line syntax when the then-case part consists of only one variable assignment and there is no else-case:

```
condition:then-case
```

For example:

```
macx:SOURCES += serial_mac.cpp
```

If we have several project files that need to share some of the same entries, we can factor out the common entries in a separate file and include it in the individual .pro files that need using it using the include() directive:

```
include(../common.pri)
```

```
HEADERS += window.h
SOURCES += main.cpp \
  window.cpp
```