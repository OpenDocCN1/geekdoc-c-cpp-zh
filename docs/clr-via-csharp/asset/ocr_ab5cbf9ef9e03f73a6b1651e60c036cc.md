are of a reference type are considered roots; value type variables are never considered roots. Now, let's look at a concrete example starting with the following class definition:

```
````csharp
internal sealed class SomeType {
    private TextWriter m_textWriter;

    public SomeType(TextWriter tw) {
        m_textWriter = tw;
    }

    public void WriteBytes(Byte[] bytes) {
        for (Int32 x = 0; x < bytes.Length; x++) {
            m_textWriter.Write(bytes[x]);
        }
    }
}
````
```

The first time the WriteBytes method is called, the just-in-time (JIT) compiler converts the method's IL code into native CPU instructions. Let's say the CLR is running on an x86 CPU, and the JIT compiler compiles the WriteBytes method into the CPU instructions shown in Figure 21-2. (I added comments on the right to help you understand how the native code maps back to the original source code.)

```
````asm
00000000 push    edi                          // Prolog
00000001 push    esi
00000002 push    ebx

EBX ─────── 00000003 mov     ebx, ecx                    // ebx = this  (argument)
            00000005 mov     esi, edx                    // esi = bytes array (argument)
ESI ─────── 00000007 xor     edi, edi                    // edi = x
            00000009 cmp     dword ptr [esi+4],0         // compare bytes.Length with 0
            0000000d jle     0000002A                    // if bytes.Length <=0, go to 2a

ECX ─────── 0000000f mov     ecx,dword ptr [ebx+4]       // ecx = m_textWriter (field)
            00000012 cmp     edi,dword ptr [esi+4]       // compare x with bytes.Length
            00000015 jae     0000002E                    // if x >= bytes.Length, go to 2e

            00000017 movzx   edx,byte ptr [esi+edi+8]   // edx = bytes[x]
            0000001c mov     eax,dword ptr [ecx]         // eax = m_textWriter's type object
            0000001e call    dword ptr [eax+000000BCh]   // call m_textWriter's Write method

            00000024 inc     edi                         // x++
            00000025 cmp     edi,dword ptr [esi+4]       // compare bytes.Length with x
            00000028 jg      0000000F                    // if bytes.Length > x, go to f

            0000002a pop     ebx                         // Epilog
            0000002b pop     esi
            0000002c pop     edi
            0000002e ret                                 // return to caller

            0000002e call    7686E337                    // Throw IndexOutOfRangeException
            00000033 int     3                           // Break in debugger
````
```

FIGURE 21-2 Native code produced by the JIT compiler with ranges of roots shown