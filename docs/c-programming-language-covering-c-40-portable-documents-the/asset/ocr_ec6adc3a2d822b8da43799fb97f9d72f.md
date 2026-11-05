# B. Grammar

This appendix contains summaries of the lexical and syntactic grammars found in the main document, and of the grammar extensions for unsafe code. Grammar productions appear here in the same order that they appear in the main document.

# B.1 Lexical Grammar

```
input:
  input-section_opt

input-section:
  input-section-part
  input-section input-section-part

input-section-part:
  input-elements_opt new-line
  pp-directive

input-elements:
  input-element
  input-elements input-element

input-element:
  whitespace
  comment
  token
```

# B.1.1 Line Terminators

+   new-line:
+   - Carriage return character (U+000D)
+   - Line feed character (U+000A)
+   - Carriage return character (U+000D) followed by line feed character (U+000A)
+   - Next line character (U+0085)
+   - Line separator character (U+2028)
+   - Paragraph separator character (U+2029)