```
: type
;
fixed_size_buffer_declarators
: fixed_size_buffer_declarator (',' fixed_size_buffer_declarator)*
;
fixed_size_buffer_declarator
: identifier '[' constant_expression ']'
;
```

End of informative text.