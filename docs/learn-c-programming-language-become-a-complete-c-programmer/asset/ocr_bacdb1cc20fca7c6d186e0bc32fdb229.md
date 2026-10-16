```
p == v)\nres.push_back(p);\nreturn res;\n}
```

# Section 4.5.1 Use of Iterators 105

The **typename** is needed to inform the compiler that C’s **iterator** is supposed to be a type and not a value of some type, say, the integer 7. We can hide this implementation detail by introducing a type alias (§3.4.5) for **Iterator**:

```
template<typename T>\nusing Iterator<T> = typename T::iterator;
```

```
template<typename C, typename V> vector<Iterator<C>> find_all(C& c, V v) {\nvector<Iterator<C>> res;\nfor (auto p = c.begin(); p!=c.end(); ++p) if (*p==v)\nres.push_back(p);\nreturn res;\n}
```

We can now write:

```
void test()\n{\nstring m {"Mary had a little lamb"}; for (auto p : find_all(m, 'a'))\nif (*p!='a')\ncerr << "string bug!\\n";\n\nlist<double> ld {1.1, 2.2, 3.3, 1.1}; for (auto p : find_all(ld,1.1)) if (*p!=1.1)\ncerr << "list bug!\\n";\n// find all occurrences of v in c\n// pisastr ing::iterator\nvector<string> vs { "red", "blue", "green", "green", "orange", "green" }; for (auto p\n: find_all(vs,"green"))\nif (*p!="green")\ncerr << "vector bug!\\n";\nfor (auto p : find_all(vs,"green"))\n*p = "vert";\n}
```

Iterators are used to separate algorithms and containers. An algorithm operates on its data through iterators and knows nothing about the container in which the elements are stored. Conversely, a container knows nothing about the algorithms operating on its elements; all it does is to supply iterators upon request (e.g., **begin()** and **end()**). This model of separation between data storage and algorithm delivers very general and flexible software.

# 4.5.2 Iterator Types