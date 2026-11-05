which has the same effect as

```
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist
```

where __clist, __c1, and __c2 are temporary variables that are otherwise invisible and inaccessible.

# 7.6.10.4 Array Creation Expressions

An array-creation-expression is used to create a new instance of an array-type.

```
array-creation-expression:
new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
new array-type array-initializer
new rank-specifier array-initializer
```

An array creation expression of the first form allocates an array instance of the type that results from deleting each of the individual expressions from the expression list. For example, the array creation expression new int[10, 20] produces an array instance of type int[,], and the array creation expression new int[10][,] produces an array of type int[] [,]. Each expression in the expression list must be of type int, uint, long, or ulong, or implicitly convertible to one or more of these types. The value of each expression determines the length of the corresponding dimension in the newly allocated array instance. Since the length of an array dimension must be non-negative, it is a compile-time error to have a constant-expression with a negative value in the expression list.

Except in an unsafe context (§18.1), the layout of arrays is unspecified.

If an array creation expression of the first form includes an array initializer, each expression in the expression list must be a constant, and the rank and dimension lengths specified by the expression list must match those of the array initializer.

In an array creation expression of the second or third form, the rank of the specified array type or rank specifier must match that of the array initializer. The individual dimension