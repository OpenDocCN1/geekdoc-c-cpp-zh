```
main:
    sub rsp, 24
    mov rdi, rsp
    mov QWORD PTR [rsp], 0   // (1)
    mov DWORD PTR [rsp+8], 0
    call fn(Agg&)            // (2)
    xor eax, eax
    add rsp, 24
    ret
```