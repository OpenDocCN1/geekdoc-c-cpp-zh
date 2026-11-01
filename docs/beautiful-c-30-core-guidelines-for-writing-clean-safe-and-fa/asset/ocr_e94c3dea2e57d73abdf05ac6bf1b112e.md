```
fn(t);        // (2)
auto u = Agg{}; // (3)
fn(u);        // (4)
t = u;        // (5)
fn(t);        // (6)
}
```

This now yields the following:

Click here to view code image

```
main:
    sub     rsp, 40
    mov     rdi, rsp
    mov     QWORD PTR [rsp], 0          // (1)
    mov     DWORD PTR [rsp+8], 0
    call    fn(Agg&)                    // (2)
    lea     rdi, [rsp+16]
    mov     QWORD PTR [rsp+16], 0       // (3)
    mov     DWORD PTR [rsp+24], 0
    call    fn(Agg&)                    // (4)
    mov     rax, QWORD PTR [rsp+16]     // (5)
    mov     rdi, rsp                    // (6)
    mov     QWORD PTR [rsp], rax        // (5)
    mov     eax, DWORD PTR [rsp+24]
    mov     DWORD PTR [rsp+8], eax
    call    fn(Agg&)                    // (6)
    xor     eax, eax
    add     rsp, 40
    ret
```

As you can see, the compiler has generated the same QWORD/DWORD trick and has emit-ted code to directly copy the memory from the original object in four instructions. Again, why would you call memcpy?