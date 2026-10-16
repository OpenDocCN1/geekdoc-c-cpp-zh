```
if (r.name .size()!=r2.name .size()) return false; for (int i = 0; i<r.name .size(); ++i)
if (toupper(r.name[i])!=toupper(r2.name[i])) return false;
return true;
}
};
```

Given that, I can define and use an unordered_set of Records:

```
unordered_set<Record,Nocase_hash,Nocase_equal> m { { "andy", 7}, {"al",9}, {"bill",-3}, {"barbara",12} }, Nocase_hash{2}, Nocase_equal{}
};
for (auto r : m)
cout << "{" << r.name << ',' << r.val << "}\n";
```

If, as is most common, I wanted to use the default values for my hash and equality functions, I could do that by simply not mentioning them as constructor arguments. By default, the unordered_set uses the default versions:

```
unordered_set<Record,Nocase_hash,Nocase_equal> m {
{"andy", 7}, {"al",9}, {"bill",-3}, {"barbara",12}
// use Nocase_hash{} and Nocase_equal{}
};
```

Often, the easiest way of writing a hash function is to use the standard-library hash functions provided as specializations of hash(§31.4.3.2). For example:

```
size_t hf(const Record& r) { return hash<string>()(r.name)^hash<int>()(r.val); };
bool eq (const Record& r, const Record& r2) { return r.name==r2.name && r.val==r2.val; };
```

Combining hash values using exclusive OR (^) preserves their distributions over the set of values of type size_t (§3.4.5, §10.3.1).
Given this hash function and equality function, we can define an unordered_set:

```
unordered_set<Record,decltype(&hf),decltype(&eq)> m {
{ {"andy", 7}, {"al",9}, {"bill",-3}, {"barbara",12} },
hf,
eq
};
for (auto r : m)
cout << "{" << r.name << ',' << r.val << "}\n";
}
```

I used decltype to avoid having to explicitly repeat the types of hf and eq.

If we don’t have an initializer list handy, we can give an initial size instead:

```
unordered_set<Record,decltype(&hf),decltype(&eq)> m {10,hf,eq};
```

That also makes it a bit easier to focus on the hash and equality operations.

If we wanted to avoid separating the definitions of hf and eq from their point of use, we