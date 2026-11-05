```
pp-declaration::
    whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
    whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line
pp-new-line::
    whitespace_opt single-line-comment_opt new-line
pp-conditional::
    pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif
pp-if-section::
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line
    conditional-section_opt
pp-elif-sections::
    pp-elif-section
    pp-elif-sections pp-elif-section
pp-elif-section::
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line
    conditional-section_opt
pp-else-section::
    whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt
pp-endif::
    whitespace_opt # whitespace_opt endif pp-new-line
conditional-section::
    input-section
    skipped-section
skipped-section::
    skipped-section-part
    skipped-section skipped-section-part
skipped-section-part::
    skipped-characters_opt new-line
    pp-directive
skipped-characters::
    whitespace_opt not-number-sign input-characters_opt
not-number-sign::
    Any input-character except #
pp-line::
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
line-indicator::
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
file-name::
    " file-name-characters "
file-name-characters::
    file-name-character
    file-name-characters file-name-character
file-name-character::
    Any input-character except " (U+0022), and new-line-character
```