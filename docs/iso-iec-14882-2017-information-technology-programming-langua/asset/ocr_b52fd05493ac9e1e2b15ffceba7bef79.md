# ISO/IEC 14882:2017(E)

```
stateT& state;
const internT* from, const internT* from_end, const internT&* from_next,
externT* to,                                     externT* to_end,                         externT&* to_next) const;
virtual result do_in(
stateT& state;
const internT* from, const externT* from_end, const externT&* from_next,
internT* to,                                     internT* to_end,                         internT&* to_next) const;
virtual result do_unshift(
stateT& state;
externT* to,                                     externT* to_end,                         externT&* to_next) const;
virtual int do_encoding(const noexcept);
virtual bool do_always_noconv(const noexcept);
virtual int do_length(stateT& state, const externT* from, const externT* end, size_t max) const;
virtual int do_max_length(const noexcept);
};
```

+   1 The class codec<internT, externT> is for use when converting from one encoding to another, such as wide characters to multibyte characters or between wide encodings such as Unicode and EUC

+   2 The specializations required in 69 (25.3.4.1.1) convert the implementation-defined native character sets, char_t, char16_t, char, mbstate_t to convert between UTF-16 and UTF-8 encoding formats, and the specialization codec<char32_t, char, mbstate_t> to convert between the UTF-32 and UTF-8 encodings. codec<wchar_t, char, mbstate_t> converts between the native character sets for narrow and wide characters. Specializations on mbstate_t perform conversion between encodings known to the library importer. Other objects of type stateT can contain any state that is used to communicate to or from the specialized do_in or out_members.

# 25.4.1.4.1 codec members

[local.codeccvt.members]

```
result out;
stateT& state;
const internT* from, const internT* from_end, const internT&* from_next,
externT* to, to_end, externT&* to_next) const;
1 Returns: do_out(state, from_end, from_next, to, to_end, to_next).
result unshift(stateT& state, externT* to, externT* to_end, externT&* to_next) const;
2 Returns: do_unshift(state, to, to_end, to_next).
result in;
stateT& state;
const externT* from, const externT* from_end, const externT&* from_next,
internT* to, internT* to_end, internT&* to_next) const;
3 Returns: do_in(state, from_end, from_next, to, to_end, to_next).
int encoding() const noexcept;
4 Returns: do_encoding().
```