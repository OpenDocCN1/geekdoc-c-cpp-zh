# Chapter Summary

```
Trying in Main() method
Trying in method A
Trying in method B
in method C
Caught in method B
Caught in method A
Caught in Main() method --
  This came from method C
Main() method is done
```

**Figure 11-38** Execution of the ReRewDemo program

If you name the Exception argument in a catch block (for example, catch (Exception) then), then you should use that identifier when you use a throw statement in the block (for example, throw e);

![](bbox=[0.104, 0.417, 0.856, 0.683])

# Chapter Summary

+   - An exception is any error condition or unexpected behavior in an executing program. In C#, all exceptions are objects that are instances of the Exception class or one of its derived classes. Most exceptions you are derived from three classes: SystemException, ApplicationException, and their parent Exception. You can purposely generate a SystemException by forcing a program to contain an error. Although you are not required to handle exceptions, you can use object-oriented techniques to provide elegant error-handling solutions.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-22