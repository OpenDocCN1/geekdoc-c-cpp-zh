
(0) `3.exe!printf`
`EAX=0x0000001b` `ECX=0x0040cc58` `EDX=0x0008e3c8`
`ESI=0x00000000` `EDI=0x00000000` `EBP=0x0018f840` `ESP=0x0018f338`
`EIP=0x00410015`
`FLAGS=20 IF`
* SEH frame at `0x18ff4c` handler=`0x771db4d` (`ntdll.dll`).
* `ExecuteHandler(0x2020+0xa3)`
* SEH frame at `0x18f9e2` prev=`0x18f878` handler=`0x004012e0` (`3.exe!`)
* except handler(3)
SEH3 frame. previouslevel=1
`scoptable(0)`. previous trylevel=1, filter=`0x00401120` (`3.exe!main+0x0`)=`0x0040a1b0` (`3.exe!main+0cb`)
`scoptable(1)`. previous trylevel=0, filter=`0x0040a1e8` (`3.exe!main+0x78`) handler=`0x00401100` (`3.exe!main+0xa9`)
* SEH frame at `0x18ff78` prev=`0x18ffc4` handler=`0x004012e0` (`3.exe!`)
except handler(3)
SEH3 frame. previous trylevel=0
`scoptable(0)`. previous trylevel=1, filter=`0x0040160d` (`3.exe!`) `mainCRTStartup(0x01b0)` handler=`0x00401621` (`3.exe!mainCRTStartup+0x1a1`)
* SEH frame at `0x18ffc4` prev=`0xffffff` handler=`0x7717f1f5` (`ntdll.dll`).
except handler(4)
SEH4 frame. previous trylevel=0
SEH4 header: `GSCookie=0xffffffff` `GSCookieXOROffset=0`
`EH=0xffffffff` `EHCookieXOROffset=0`
`scoptable(0)`. previous trylevel=-2, filter=`0x771f79e0` (`ntdll.dll!` `safe_se_handle_table+0x20`) handler=`0x771febeb0` (`ntdll.dll!` `TTerminateProcess+0x4+0xa3`)
* SEH frame at `0x18fffe4` prev=`0xffffffff` handler=`0x77247428` (`ntdll.dll!`) `FinalExceptionHandlerHandler(0xb6)`

# SEH4

在缓冲区溢出期间（第 340 页 1.26），作用域表的地址可能会被重写。从 MSVC 2005 开始，SEH3 被升级为 SEH4 以提供缓冲区溢出保护。指向作用域表的指针现在与一个安全令牌（security cookie）进行异或运算。作用域表被扩展，包含一个由两个安全令牌指针组成的头部。

每个元素在栈内部都有另一个值的偏移量：栈帧地址（`EBP`）与安全令牌进行异或后，放置在栈中。

该值将在异常处理期间被读取并检查其正确性。栈中的安全令牌每次都是随机的，因此我们希望远程攻击者无法预测它。

SEH4 中的初始上一层级（previous try level）是 -2 而不是 -1。

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的邮箱。谢谢！

# 栈

![](img/4590a0c34d3b5b6ca77b4202d4036d48_1012_0.png)

## 作用域表

| GS Cookie Offset | |
| :--- | :--- |
| GS Cookie XOR Offset | |
| EH Cookie Offset | |
| EH Cookie XOR Offset | ... |

### 关于第一个 try/except 块的信息

| 0xFFFFFF (-1) | |
| :--- | :--- |
| filter 函数 | |
| handler/finally 函数 | |

### 关于第二个 try/except 块的信息

| 0 | |
| :--- | :--- |
| filter 函数 | |
| handler/finally 函数 | |

### 关于第三个 try/except 块的信息

| 1 | |
| :--- | :--- |
| filter 函数 | |
| handler/finally 函数 |

... 更多条目

都是在 MSVC 2012 中使用 SEH 编译的示例：

### 列表 6.31: MSVC 2012: 一个 try 示例

```
$SG0845 DB 'hello #1!', 0AH, 0H
$SG0846 DB 'hello #2!', 0AH, 0H
$SG0848 DB 'access violation, can't recover',
```

| 作用域表: xdata$ | |
| :--- | :--- |
| `_table_main DD 0xFFFFFFFF` | GS Cookie Offset |
| `DD 0H` | GS Cookie XOR Offset |
| `DD ffffffcH` | EH Cookie Offset |
| `DD 0H` | EH Cookie XOR Offset |
| `DD ffffffeH` | previous level |
| `DD FLAT12@main` | filter |
| `DD FLAT8@main` | handler |

```
xdata$

$T2 = -36; size = 4
$T3 = -32; size = 4
$T6 = -28; size = 4
$EHRecs = -24; size = 24

main PROC
push    ebp
mov     ebp, esp
push    -2
push    OFFSET tableable
push    OFFSET except_handler
mov     eax, DWORD PTR fs:0
push    eax
add     esp, -20
push    ebx
push    esi
mov     edi
mov     eax, DWORD PTR security cookie
xor     DWORD $$EHRecs[ebp+16], eax ; 异或后的指针
xor     eax, ebp
push    eax
lea     eax, DWORD PTR $$EHRecs[ebp+] ; security_cookie
EXCEPTION REGISTRATION RECORD
mov     DWORD fs:0, eax
mov     DWORD $$EHRecs[ebp], esp
mov     DWORD [$ebp], 0
mov     DWORD $$EHRecs[ebp+20], 0 // previous level
push    OFFSET'hello #1!'
call    printf
add     esp, 4
mov     eax, DWORD PTR $[ebp]
mov     DWORD [eax], 1
push    OFFSET $$EHRecs[ebp+20], -2 // previous level
call    printf
add     esp, 4
mov     DWORD PTR $[ebp
mov     DWORD PTR SHORT LN6@main
ret

; filter:
$LN7@main:
$LN12@main:
mov     ecx, DWORD PTR $$EHRecs[ebp+4]
mov     DWORD PTR [ecx]
mov     eax, DWORD PTR [edx]
mov     DWORD PTR $T[2], eax
cmp     DWORD PTR $[T2], -1073741819 // C0000005H
jne     SHORT LN4@main
mov     DWORD PTR tv6[ebp], 1
```

如果你发现任何拼写错误、错误或任何建议，请随时给我留言：我的邮箱。谢谢！

# 列表 6.32: MSVC 2012: 两个块示例

```
$S6GB5486 DB 'in filter, code=0%00X', 0AH, 0H
$S6GB5488 DB 'yes, that is our exception', 0AH, 0H
$S6GB5490 DB 'not our exception', 0AH, 0H
$S6GB5497 DB 'hello!', 0AH, 0H
$S6GB5499 DB '0x11233 raised. now let's crash', 0AH, 0H
$S6GB5501 DB 'access violation, can't recover', 0AH, 0H
$S6GB5503 DB 'user exception catch', 0AH, 0H
```

```
xdata$   SEGMENT
DD 0xFFFFFFFF | GS Cookie Offset |
_table_main DD 0H | GS Cookie XOR Offset |
DD ffffffcH | EH Cookie Offset |
DD 0H | EH Cookie XOR Offset |
DD ffffffeH | previous level |
DD FLAT12@main | filter
DD FLAT8@main | handler

xdata$

$T2 = -36; size = 4
$T3 = -32; size = 4
$T6 = -28; size = 4
$EHRecs = -24; size = 24

main PROC
push    ebp
mov     ebp, esp
push    -2; initial try level
push    OFFSET tableable
push    OFFSET except_handler
mov     eax, DWORD PTR fs:0
push    eax
add     esp, -20
push    ebx
push    esi
mov     edi
mov     eax, DWORD PTR security cookie
xor     DWORD $$EHRecs[ebp+16], eax // 异或后的指针
xor     eax, ebp
push    eax
lea     eax, DWORD PTR $$EHRecs[ebp+] // security_cookie
EXCEPTION REGISTRATION RECORD
mov     DWORD fs:0, eax
mov     DWORD $$EHRecs[ebp], esp
mov     DWORD [$ebp], 0
mov     DWORD $$EHRecs[ebp+20], 0 // previous level
push    OFFSET  'hello #1!'
call    printf
add     esp, 4
mov     eax, DWORD PTR $[ebp]
mov     DWORD [eax], 1
push    OFFSET $$EHRecs[ebp+20], -2 // previous level
call    printf
add     esp, 4
mov     DWORD PTR $[ebp
mov     DWORD PTR SHORT LN6@main
ret
```

```
mov     DWORD PTR tv72[ebp], 1
jmp     SHORT $LN6@main
$LN5@main:
mov     DWORD PTR tv72[ebp], 0
$LN6@main:
mov     eax, DWORD PTR tv72[ebp]
$LN14@main:
$LN16@main:
ret     0

; 内部块处理器：
$LN13@main:
mov     esp, DWORD PTR $SEHRec$[ebp]
push    OFFSET $SGB5501 ; 'access violation, can't recover'
call    _printf
add     esp, 4
mov     DWORD PTR $SEHRec$[ebp+20], 0 ; 退出内部 try 块，将之前的 try 级别置回 0
$LN22@main:
mov     DWORD PTR $SEHRec$[ebp+20], -2 ; 退出两个块，将之前的 try 级别置回 -2
jmp     SHORT $LN7@main

; 外部块过滤器过滤器：
$LN8@main:
$LN19@main:
mov     ecx, DWORD PTR $SEHRec$[ebp+4]
mov     edx, DWORD PTR [ecx]
mov     eax, DWORD PTR [edx]
mov     DWORD PTR $T2$[ebp], eax
mov     ecx, DWORD PTR _$SEHRec$[ebp+4]
push    ecx
mov     edx, DWORD PTR $T2$[ebp]
push    edx
call    _filter_user_exceptions
add     esp, 8
$LN10@main:
$LN17@main:
ret     0

; 外部块处理器：
$LN9@main:
mov     esp, DWORD PTR $SEHRec$[ebp]
push    OFFSET $SGB5503 ; 'user exception caught'
call    _printf
add     esp, 4
mov     DWORD PTR $SEHRec$[ebp+20], -2 ; 退出两个块，将之前的 try 级别置回 -2
$LN7@main:
xor     eax, eax
mov     ecx, DWORD PTR $SEHRec$[ebp+8]
mov     DWORD PTR fs:0, ecx
pop     ecx
pop     edi
```

如果你发现任何拼写错误、错误或有任何建议，请随时给我写信：[我的邮箱]。谢谢！

| pop | esi |
| pop | ebx |
| mov | esp, ebp |
| pop | ebp |
| ret | 0 |
| main | ENDP |

```asm
code$ = 8          ; size = 4
_eps$ = 12         ; Size = 4
.filter_user_exceptions PROC
push    ebp
mov     esp, ebp
mov     eax, DWORD PTR __code$[ebp]
push    eax
push    OFFSET $SSG5486 ; 'in filter.code:0x008X'
call    _printf
add     esp, 8
cmp     SHORT $LN2@filter_user
jne     SHORT $LN2@filter_user ; '是的，那是我们的异常'
push    _printf
call    _printf
add     esp, 4
mov     eax, 1
jmp     SHORT $LN3@filter_user
mov     SHORT $LN3@filter_user
$LN2@filter_user:
push    OFFSET $SSG5490 ; '不是我们的异常'
call    _printf
add     esp, 4
xor     eax, eax
$LN3@filter_user:
pop     ebp
ret     0
filter_user_exceptions ENDP
```
