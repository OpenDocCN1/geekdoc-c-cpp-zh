# Calling Conventions

```
add eax, edx
pop ebp
ret
and
push 3
push 2
call _MyFunction
add esp, 8
```

When translated to assembly code, CDECL functions are almost always prepended with an underscore (that's why all previous examples have used '_' in the assembly code).

# 11.3.2 STDCALL

STDCALL also known as 'WINAPI (and a few other names, depending on where you are reading it) is almost exclusively claimed by Microsoft as the standard calling convention for the Win32 API. Since STDCALL is strictly defined by Microsoft, all compilers that implement it the same way.

+   * STDCALL passes arguments right-to-left, and returns the value in eax. (The Microsoft documentation erroneously claimed that arguments are passed left-to-right, but this is not the case).
* The called function cleans the stack, unlike CDECL. This means that STDCALL doesn't allow variable-length argument lists.

Consider the following function:

```
_stdcall int MyFunction2(int a, int b)
{
    return a + b;
}
```

and the calling instruction:

```
x = MyFunction2(2, 3);
```

These will produce the respective assembly code fragments:

```
:_MyFunction08
push ebp
mov ebp, esp
mov eax, [ebp + 8]
mov edx, [ebp + 12]
add eax, edx
pop ebp
ret
```

```
and
push 3
push 2
call _MyFunction08
```

There are a few important points to note here: