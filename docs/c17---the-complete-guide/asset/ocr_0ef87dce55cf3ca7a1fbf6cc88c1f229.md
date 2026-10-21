# 20.3 Path Operations

• Only different formats for specifying a directory separator are detected. Thus, the following paths are all equal (provided the backslash is a valid directory separator):

```
tmp1/f
/tmp1/f
/tmp1\f
tmp1\ /f
```

It is only if you call lexically_normal() for each path that all of the paths above are equal (provided the backslash is a valid directory separator). For example:

```
std::filesystem::path p1{"tmp1/f"};
std::filesystem::path p2{"../tmp1/f"};
```

```
p1 == p2 //true
p1.compare(p2) //not 0
p1.lexically_normal() == p2.lexically_normal() //true
p1.lexically_normal().compare(p2.lexically_normal()) //0
```

If you want to take the filesystem into account so that symbolic links are handled correctly, you can use equivalent(). However, note that this function requires that both paths represent existing files. Thus, a generic way to compare paths as accurately as possible (which does not have the best performance) is as follows:

```
bool pathsAreEqual(const std::filesystem::path& p1, const std::filesystem::path& p2)
{
	return exists(p1) && exists(p2) ? equivalent(p1, p2)
		: p1.lexically_normal() == p2.lexically_normal();
}
```

# 20.3.7 Other Path Operations

Table Other Path Operations lists the remaining path operations not listed yet.

| Call | Effect |
|------|--------|
| p.hash_value() | Yields the hash value for a path |

Note that only equal paths are guaranteed to have the same hash value. The following paths yield different hash values:

+   tmp1/f
+   ./tmp1/f
+   /tmp1/. /f
+   tmp1/tmp11/.. /f

Therefore, you might want to normalize paths before you put them in a hash table.