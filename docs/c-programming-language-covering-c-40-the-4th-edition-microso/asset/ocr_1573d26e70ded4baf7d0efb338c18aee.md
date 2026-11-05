# B.1.2 Comments

```
comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt

input-characters:
  input-character
  input-characters input-character

input-character:
  Any Unicode character except a new-line-character

new-line-character:
  Carriage return character (U+000D)
  Line feed character (U+000A)
  Next line character (U+0085)
  Line separator character (U+2028)
  Paragraph separator character (U+2029)

delimited-comment:
  /* delimited-comment-text_opt asterisks /

delimited-comment-text:
  delimited-comment-section
  delimited-comment-text delimited-comment-section

delimited-comment-section:
  /
  asterisks_opt not-slash-or-asterisk

asterisks:
  *
  asterisks *

not-slash-or-asterisk:
  Any Unicode character except / or *
```