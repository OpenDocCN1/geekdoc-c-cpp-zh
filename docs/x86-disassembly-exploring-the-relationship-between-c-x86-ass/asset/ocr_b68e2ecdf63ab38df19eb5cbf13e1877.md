```
push	eecx
; Line 11
mov	eax, DWORD PTR tv64[ebp]
mov	DWORD PTR tv64[ebp], eax
mov	eax, DWORD PTR tv64[ebp]
sub	cx, 1
mov	eax, DWORD PTR tv64[ebp]
mov	dWORD PTR tv64[ebp], 3
ja	SHORT $L810
mov	eax, DWORD PTR tv64[ebp]
mov	DWORD PTR $L818[esp+4]
jmp
$L806:	1
; Line 14
push	push
call	_MyFunction
add	esp, 4
; Line 15
jmp	SHORT $L803
$L807:	2
; Line 17
push	push
call	_MyFunction
add	esp, 4
; Line 18
jmp	SHORT $L803
; Line 19
push	3
call	_MyFunction
add	esp, 4
; Line 20
jmp	SHORT $L803
$L809:	4
; Line 22
push	4
call	_MyFunction
add	esp, 4
; Line 23
jmp	SHORT $L803
$L810:	5
; Line 25
push	5
call	_MyFunction
add	esp, 4
$L803:
; Line 27
xor	eax, eax
; Line 28
mov	esp, ebp
pop	ebp
ret	0
$L818:
DD	$L806
DD	$L807
DD	$L808
DD	$L809
_main	ENDB
```

Lets work our way through this. First, we see that line 10 sets up our standard stack frame, and it also saves exc. Why does it save exc? Scanning the function, we never see a corresponding 'pop exc' instruction, so it seems that the value is never restored at all. In fact, the compiler isn't saving exc at all, but is simply reserving space on the stack: it's creating a local variable. The original C code didn't have any local variables, however, so perhaps the compiler needed some extra scratch space to store intermediate values. Why doesn't the compiler execute the more familiar 'sub esp, 4' command to create the