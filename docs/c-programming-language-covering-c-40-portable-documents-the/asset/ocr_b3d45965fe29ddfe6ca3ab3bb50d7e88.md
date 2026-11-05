Once the candidate function members and the argument list have been identified, the selection of the best function member is the same in all cases:

+   - Given the set of applicable candidate function members, the best function member in that set is located. If the set contains only one function member, then that function member is the best function member. Otherwise, the best function member is the one function member that is better than all other function members with respect to the given argument list, provided that each function member is compared to all other function members using the rules in §7.5.3.2. If there is not exactly one function member that is better than all other function members, then the function member invocation is ambiguous and a binding-time error occurs.

The following sections define the exact meanings of the terms applicable function member and better function member.

> > **BILL WAGNER** This section gets very complicated. As you read it, remember that every additional overload you create may contribute to the possible ambiguity in overload resolution. You should limit yourself to the number of overloads that truly make it easier on your users. That approach will keep matters as simple as possible for users of your class and help them ensure that they get the right method.

# 7.5.3.1 Applicable Function Member

> > **VLADIMIR RESHETNIKOV** This section also governs applicability of delegates (§7.6.5.3).

A function member is said to be an applicable function member with respect to an argument list A when all of the following are true:

+   - Each argument in A corresponds to a parameter in the function member declaration as described in §7.5.1.1, and any parameter to which no argument corresponds is an optional parameter.
+   - For each argument in A, the parameter passing mode of the argument (i.e., value, ref, or out) is identical to the parameter passing mode of the corresponding parameter, and
+     - For a value parameter or a parameter array, an implicit conversion (§6.1) exists from the argument to the type of the corresponding parameter, or
+     - For a ref or out parameter, the type of the argument is identical to the type of the corresponding parameter. After all, a ref or out parameter is an alias for the argument passed.