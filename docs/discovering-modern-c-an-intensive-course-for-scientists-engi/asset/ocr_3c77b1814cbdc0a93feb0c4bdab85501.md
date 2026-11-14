# 1.2.4.3 Hiding

When a variable with the same name exists in nested scopes, then only one variable is visible. The variable in the inner scope hides the homonymous variables in the outer scopes. For instance:

```
int main ()
{
    int a = 5;        // define a#1
    {
        a = 3;        // assign a#1, a#2 is not defined yet
        int a;        // define a#2
        a = 8;        // assign a#2, a#1 is hidden
    }                 // end of a#2's scope
    a = 7;            // assign to a#1 (a#2 out of scope)
}
    a = 11;
    // assign to a#1 (a#2 out of scope)
}
    return 0;
}
```

Due to hiding, we must distinguish the lifetime and the visibility of variables. For instance, a#1 lives from its declaration until the end of the main function. However, it is only visible from its declaration until the declaration of a#2 and again after closing the block containing a#2. In fact, the visibility is the lifetime minus the time when it is hidden.

Defining the same variable name twice in one scope is an error.

The advantage of scopes is that we do not need to worry about whether a variable is already defined somewhere outside the scope. It is just hidden but does not create a conflict.3 Unfortunately, the hiding makes the homonymous variables in the outer scope inaccessible. We can cope with this to some extent with clever renaming. A better solution, however, to manage nesting and accessibility is namespaces; see Section 3.2.1.

static variables are the exception that confirms the rule: they live till the end of the execution but are only visible in the scope. We are afraid that their detailed introduction is more distracting than helpful at this stage and have postponed the discussion to Section A.2.2.

# 1.3 Operators

C++ is rich in built-in operators. There are different kinds of operators:

+   - Computational:
+     - Arithmetic: +, -, *, %, ...