Sometimes we want to sort `vr` by name, and sometimes we want to sort it by address. Unless we can do both elegantly and efficiently, our techniques are of limited practical interest. Fortunately, doing so is easy. We can write

```
// ... sort(vr.begin(), vr.end(), Cmp_by_name()); // sort by name // ... sort(vr.begin(), vr.end(), Cmp_by_addr()); // sort by addr // ...
```

**Cmp_by_name** is a function object that compares two **Records** by comparing their **name** members. **Cmp_by_addr** is a function object that compares two **Records** by comparing their **addr** members. To allow the user to specify such comparison criteria, the standard library **sort** algorithm takes an optional third argument specifying the sorting criteria. **Cmp_by_name**() creates a **Cmp_by_name** for **sort**() to use to compare **Records**. That looks OK – meaning that we wouldn't mind maintaining code that looked like that. Now all we have to do is to define **Cmp_by_name** and **Cmp_by_addr**:

```
// different comparisons for Record objects: struct Cmp_by_name { bool operator()(const Record& a, const Record& b) const { return a.name < b.name; } }; struct Cmp_by_addr { bool operator()(const Record& a, const Record& b) const { return strncmp(a.addr, b.addr, 24) < 0; } };
```

The **Cmp_by_name** class is pretty obvious. The function call operator, **operator**(), simply compares the **e_name** strings using the standard **string**'s **<** operator. However, the comparison in **Cmp_by_addr** is ugly. That is because we chose an ugly representation of the address: an array of 24 characters (not zero terminated). We chose that partly to show how a function object can be used to hide ugly and error-prone code and partly because this particular representation was once presented to me as a challenge: “an ugly and important real-world problem that the STL can't handle.” Well, the STL could. The comparison function uses the standard C (and C++) library function **strncmp**() that compares fixed-length character arrays, returning a negative number if the second “string” comes lexicographically after the first. Look it up should you ever need to do such an obscure comparison (e.g., §B.11.3).