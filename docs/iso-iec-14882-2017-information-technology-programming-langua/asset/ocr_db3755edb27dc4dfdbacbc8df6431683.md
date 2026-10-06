# ISO/IEC 14882:2017(E)

```
explicit messages(size_t refs = 0);

catalog open(const basic_string<char>& fn, const locale& loc) const;
string_type get(catalog c, int set, int msgid,
    const string_type& default) const;
void close(catalog c) const;

static locale::id id;
```

```
protected:
    messages();
    virtual catalog do_open(const basic_string<char>&, const locale& loc) const;
    virtual string_type do_get(catalog int, int set, int msgid,
        const string_type& default) const;
    virtual void do_close(catalog c) const;
```

+   1 Values of type messages_base::catalog usable as arguments to get and close can be obtained by calling member open.

# 25.4.7.1 messages members [locale.messages.members]

```
catalog open(const basic_string<char>&, const locale& loc) const;
```

+   1 Returns: do_open(name, loc).

```
string_type get(catalog cat, int set, int msgid, string_type& default) const;
```

+   2 Returns: do_get(cat, set, msgid, default).

```
void close(catalog cat) const;
```

+   3 Effects: Calls do_close(cat).

# 25.4.7.2 messages virtual functions [locale.messages.virtuals]

```
catalog do_open(const basic_string<char>&, const locale& loc) const;
```

+   1 Returns: A value that may be passed to get() to retrieve a message from the message catalog identified by the string name according to an implementation-defined mapping. The result can be used until it is passed to close().

+   2 Returns a value less than 0 if no catalog can be opened.

+   3 Remarks: The locale argument is used for set conversion when retrieving messages, if needed.

```
string_type do_get(catalog cat, int set, int msgid, const string_type& default) const;
```

+   4 Requires: cat shall be a catalog obtained from open() and not closed.

+   5 Returns: A message identified by arguments set, msgid, and default, according to an implementation-defined mapping. If no such message can be found, returns default.

```
void close(catalog cat) const;
```

+   6 Requires: cat shall be a catalog obtained from open() and not yet closed.

+   7 Effects: Releases unspecified resources associated with cat.

+   8 Remarks: The limit on resources, if any, is implementation-defined.