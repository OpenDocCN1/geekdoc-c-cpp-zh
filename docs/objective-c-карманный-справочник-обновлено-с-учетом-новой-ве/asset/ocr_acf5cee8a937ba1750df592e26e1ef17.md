# CHAPTER 11: Key-Value Coding

a key or key path and have it automatically retrieve the data from the model, without needing to know any details of the model’s implementation, or even its interface beyond the fact that it supports KVC.

# Accessing Values by Key

```
[object setValue: @"42"
forKey: @"integer";
int value = 
[[object valueForKey: @"integer"]
intValue];nNSAssert(value == 42,
@"Value set and retrieved")];
```

> From: kvc.m

Objects manipulated via KVC look much like dictionaries. The NSDictionary class is, itself, KVC compliant, although you typically don’t use the KVC methods when using it.

The two most common methods for interacting with KVC-compliant objects are -valueForKey and -setValue:forKey:. The -objectForKey method on NSDictionary behaves almost the same way for retrieving values. The two set methods on NSDictionary work slightly differently.

The first thing you will notice is that you get a compile-time warning if you use -setObject:forKey: on an immutable dictionary. You won’t if you