# # A.8 Operations

# ## A.8.1 Types of operation

The arithmetic operators are:

+   - @(a + b) (Addition)
+   - @(a - b) (Subtraction)
+   - @(a * b) (Multiplication)
+   - @(a / b) (Division)

The logical operators are:

+   - @(!a) (Not boolean)
+   - @(a|b) (Or)
+   - @(a&b) (And)

The equality operators are:

+   - @(token1==token2) (Equality)
+   - @(token1!=token2) (Non-equality)
+   - @(token1<token2) (Less-than)
+   - @(token1>token2) (Greater-than)

The conditional operators are:

+   - @(boolval ? iftrue : iffalse) (If)
+   - @(testval =A : 1 B : 2 else : 0) (Case)

# ## A.8.2 Retrieving data values

The attribute values for a given data definition in an ACD file can depend on the values from other data definitions. It is possible to retrieve the value of:

+   - A data definition (application parameter)
+   - An attribute of a data definition
+   - A calculated attribute of a data definition
+   - An ACD variable definition.

Such values are retrieved using the ACD ‘get the value of’ syntax which consists of a term ParameterName.AttributeName term surrounded by parentheses with a dollar sign ($) at the front:

```
$ (ParameterName.AttributeName)
```

If just the value of the data definition is to be retrieved, the AttributeName component is omitted: