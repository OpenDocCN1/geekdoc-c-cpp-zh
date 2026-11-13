# isempty()

```
Algorithm of isempty() function –
begin procedure isempty
if top less than 1 return true
else
return false
endif
end procedure
```

Implementation of isempty() function in C programming language is slightly different. We initialize top at -1, as the index in array starts from 0. So we check if the top is below zero or -1 to determine if the stack is empty. Here’s the code –

```
bool isempty() { if(top == -1) return true; else return false; }
```