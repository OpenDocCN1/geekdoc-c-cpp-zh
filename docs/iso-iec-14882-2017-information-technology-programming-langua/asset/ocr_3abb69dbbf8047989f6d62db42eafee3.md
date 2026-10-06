# ISO/IEC 14882:2017(E)

# 25.4.5.3.1  time_put members

```
iter_type put(iter_type s, ios_base* str, char_type fill, const tm* t,
              const char* pattern, const char* pat_end) const char* end) const;
iter_type put(iter_type s, ios_base* str, char_type fill, const tm* t,
              char format, char modifier = 0) const;
```

+   1. Effects: The first step through the sequence from pattern to pat, identifying characters that are part of a format sequence. Each character that is not part of a sequence is returned immediately, and each sequence, as it is identified, results in a call to do_put; thus elements and other characters are interleaved in the order in which they appear in the format. Sequences are identified by converting each character to a char value, if it differs from the sequence. The first character of each sequence is equal to 'Q', followed by an optional modifier char mod^245 and a format character spec as defined for the strftime. If no modifier is present, mod is zero. For each valid format sequence, call do_put(s, str, fill, t, format, modifier).
2. The second call do_put returns the last character produced.
3. [Note: The argument may be used in the implementation-defined formats or by derivations. A space character is a reasonable default for this argument. — end note]
4. Returns: An iterator pointing immediately after the last character produced.

# 25.4.5.3.2  time_put_virtual

```
iter_type do_put(iter_type s, ios_base* str, char_type fill, const tm* t,
              char format, char modifier) const;
```

+   1. Effects: Formatting the contents of the parameter t placed on the output sequence s; ct_name is produced by the parameters format and modifier, interpreted as the format string in the standard library function strftime^246, except that the sequence of characters produced for those specifies are as depending on the C locale are or instead implementation-defined^247
2. Returns: An iterator pointing immediately after the last character produced. [Note: The fill argument may be used in the implementation-defined formats or by derivations. A space character is a reasonable default for this argument. — end note]

# 25.4.5.4  Class template_put_byname

```
namespace std {
template <class charT, class OutputIterator = ostreambuf_iterator<charT>>
class time_put_byname : public_put<charT, OutputIterator> {
public:
  using char_type = charT;
  using iter_type = OutputIterator;

  explicit time_put_byname(const char* str, size_t refs = 0);
  explicit time_put_byname(const string str, size_t refs = 0);

protected:
  time_put_byname();
};
```

245) The C programming language defines no modifiers, most vendors do.
246) Interpretation of the modifier argument is implementation-defined, but should follow POSIX conventions.
247) Implementations should refer to other standards such as POSIX for these definitions.

§ 25.4.5.4  ©/IEC 2017 - All rights reserved  814