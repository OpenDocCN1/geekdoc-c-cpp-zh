```
bool find_from_addr(const Message* m, string& s)
{
	for (const auto& x : *m)
		if (int n = is_prefix(x, "From: ")) {
			s = string(x,n);
			return true;
		}
	return false;
}
```

```
string find_subject(const Message* m)
{
	for (const auto& x : *m)
		if (int n = is_prefix(x, "Subject: ")) return string(x,n);
	return "";
}
```

Note the way we use substrings: `string(s,n)` constructs a string consisting of the tail of **s** from `s[n]` onward (`s[n]..s[size()-1]`), whereas `string(s,0,n)` constructs a string consisting of the characters `s[0]..s[n-1]`. Since these operations actually construct new strings and copy characters, they should be used with care where performance matters.

Why are the `find_from_addr()` and `find_subject()` functions so different? For example, one returns a **bool** and the other a **string**. They are different because we wanted to make a point:

+   - `find_from_addr()` distinguishes between finding an address line with an empty address ("") and finding no address line. In the first case, `find_from_addr()` returns `true` (because it found an address) and sets **s** to "" (because the address just happens to be empty). In the second case, it returns `false` (because there was no address line).
- `find_subject()` returns "" if there was an empty subject or if there was no subject line.

Is the distinction made by `find_from_addr()` useful? Necessary? We think that the distinction can be useful and that we definitely should be aware of it. It is a distinction that comes up again and again when looking for information in a data file: did we find the field we were looking for and was there something useful in it? In a real program, both the `find_from_addr()` and `find_subject()` functions would have been written in the style of `find_from_addr()` to allow users to make that distinction.

This program is not tuned for performance, but it is probably fast enough for most uses. In particular, it reads its input file only once, and it does not keep