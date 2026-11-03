example, in the following statement, only second PI will be replaced
by the value defined

by preprocessor PI.

```
```c
printf(" PI == %fn ", PI);
```
```

The program becomes more readable by using preprocessors. It
makes easy to follow the

flow of program. More importantly, if a constant has been defined
symbolically by

means of the #define facility and used throughout a program, it is
easy to change it later,

if necessary. For example, the letter c is universally accepted to be
used to represent the

speed of light, which is approximately 299792.458 lan/sec. If we
write the following

preprocessor and then use the letter C throughout tens of thousands
of lines of code to

represent symbolically the constant 299792.458, it will be easy to
change the code when

a new physical experiment produces a better value for the speed of
light. All the code is

updated by simply changing the constant in the #define line. Such
are the advantages of

using preprocessors.

```
```c
#define C 299792.458
```
```