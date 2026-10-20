So far, we have nothing to optimize in this program. The current state is that we have two vectors, v and coll1, and two strings, s and its copy, which is the first element in coll1. They should all be separate objects with their own memory for the value, because modifying one of them should not impact any of the other objects.

+   • Let us now look at the next statement, which creates a new temporary string and again inserts it into the vector:
+   coll.push_back(s+s);

This statement is performed in three steps:

+   1. We create the temporary string s+s:

```
std::vector<std::string> createAndInsert()
{
	std::vector<std::string> coll;
	coll.reserve(3);
	std::string s = "data";
	coll.push_back(s);
	coll.push_back(s+s);
	coll.push_back(s);
	return coll;
}

std::vector<std::string> v;
...

v = createAndInsert();
```

![](bbox=[0.48, 0.38, 0.95, 0.58])

2. We insert this temporary string into the vector coll1. As always, the container creates a copy of the passed value, which means that we create a deep copy of the temporary string, including allocating memory for the value:

![](bbox=[0.48, 0.72, 0.95, 0.92])