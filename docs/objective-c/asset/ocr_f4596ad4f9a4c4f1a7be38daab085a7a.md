Finally, when you are no longer using an associated object, you can remove the association by again calling the Objective-C function objc_setAssociatedObject, but in this case passing nil as the value to be associated.

In all cases, the key associated with the value must be unique to that value. The actual data type of the key is a void *. Typically, you want to use a variable which has been declared to be static for this key. By doing so, you are ensured that the pointer associated with the key will always point to a singular instance of that pointer and be unique.

The association policy can be one of the following values, as shown in Table 8.1

# Table 8.1

| Value | Purpose |
|---|---|
| OBJC_ASSOCIATION_ASSIGN | Specifies the value will simply be assigned. No retain or release will be used. |
| OBJC_ASSOCIATION_RETAIN_NONATOMIC | Specifies the value will be assigned and retained in a non-threadsafe way. |
| OBJC_ASSOCIATION_COPY_NONATOMIC | Specifies the value will be copied in a non-threadsafe way. |
| OBJC_ASSOCIATION_RETAIN | Specifies the value will be assigned and retained in a threadsafe way. |
| OBJC_ASSOCIATION_COPY | Specifies the value will be copied in a threadsafe way. |

As you can see, these values closely resemble the property attributes that can be specified when declaring properties for objects. It uses much the similar mechanism for associative references.

As an example of how an associative reference actually works in code, Listing 8.8 shows a category declared on NSMutableDictionary, which will maintain a cached, sorted list of the dictionaries keys. There are several methods defined here for housekeeping purposes. If you were actually implementing this category, there might be better ways to do it. The purpose here is simply to illustrate the lifecycle of the associative reference which will be used to store the sorted keys.

# Listing 8.8

# A sorted keys category

```
@interface NSMutableDictionary (SortedKeys)

- (void)generateSortedKeys;
- (NSArray *)sortedKeys;
- (void)dropSortedKeys;
```