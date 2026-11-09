# ### 7.3 Macro Call

By now, it should be clear that the main difference between a macro call and a subprogram call is that the level of local variables changes with a macro call, but it does not change with a subprogram call. Moreover, a macro call can pass data to the called program, whereas a subprogram call does not have this capability.

A subprogram is called by M98 and M198. A macro can be called using any of the following methods:

+   * Simple call (G65)
+   * Modal call (G66)
+   * Call with user-defined G-code
+   * Call with user-defined M-code

Those who are new to macro programming may skip the last two methods of calling a macro, at this stage. Even the modal call (G661) is not very frequently used. G65 can be used for calling any macro, without any limitation. Other methods do provide some convenience, but one can manage with G65 also. However, one must know all the methods because of the specific advantages these offer. Moreover, any method may have been used in the programs developed by other programmers, which one can understand only if one knows the method used. However, in the interest of a steeper learning curve, one may choose to read about G65 only. The remaining methods can be learned at a later stage. One may skip Sec. 7.4 also.

# ### Simple Call (G65)

The syntax of macro call with G65 is

```
```
G65 P<program number> L<repetition count> <argument 1>
. . . <argument n>
```
```

The program number is the number of an existing program that is to be called. Usually, 8000 or 9000 series numbers are used as macro-program numbers, since these can be protected from accidental editing/deletion, through parameters 3202#0 and 3202#4, respectively. However, any legal program number (1 to 9999) can be used.

Repetition count, which defaults to one (i.e., L1 can be omitted), is the number of successive executions of the called macro. This is the only way a macro can be repeatedly executed. The repetition count of a macro cannot be included in the P-word, unlike what can be done for repeating a subprogram call. As explained in Chap. 6, the repetition count of a subprogram can be included in the P-word also (apart from the L-word method). Here, the P-word is used only for specifying the program number. Up to 9999 macro repetitions are possible.