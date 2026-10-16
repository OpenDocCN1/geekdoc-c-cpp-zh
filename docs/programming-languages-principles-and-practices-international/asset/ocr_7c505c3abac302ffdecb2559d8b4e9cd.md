```
```cpp
(7)   displayMessage(t.error_message);
(8)   ...
(9)   }
(10)  catch (Big_Trouble b)
(11)  { // handle big trouble, if possible
(12)  ...
(13)  }
(14)  catch (...) // actually three dots here, not an ellipsis!
(15)  { // handle any remaining uncaught exceptions
(16)  }
```
```

**Figure 9.10** A C++ try-catch block

Here the compound statement after the reserved word *try* is required (the curly brackets on lines 2 and 4 of Figure 9.10), and any number of *catch* blocks can follow the initial *try* block. Each *catch* block also requires a compound statement and is written as a function of a single parameter whose type is an exception type (which can be any class or structure type). The exception parameter may be consulted to retrieve appropriate exception information, as in line 7 of Figure 9.10. Note also in Figure 9.10 the catch-all catch block at the end that catches any remaining exceptions, as indicated by the three dots inside the parentheses on line 14.

The syntax of try-catch blocks in C++ is really overkill, since catch blocks could have been associated with any statement or block. Indeed, in Ada and ML that is exactly the case. For example, in Ada the reserved word *exception* is reused to introduce handlers. Handles can appear at the end of any block, as shown in Figure 9.11, which contains Ada code corresponding to the C++ code of Figure 9.10. Note also the similarity of the syntax of the exception list (lines 5–13 of Figure 9.11) to that of the Ada case statement.

```
```ada
(1)   begin
(2)   -- try to perform some processing
(3)   ...
(4)   exception
(5)       when Trouble =>
(6)           --handle trouble, if possible
(7)           displayMessage("trouble here!");
(8)           ...
(9)       when Big_Trouble =>
(10)          -- handle big trouble, if possible
(11)          ...
(12)      when others =>
(13)          -- handle any remaining uncaught exceptions
(14)  end;
```
```

**Figure 9.11** An Ada try-catch block corresponding to Figure 9.9