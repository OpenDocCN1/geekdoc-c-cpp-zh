# EXPROC.ASM

```
CODE_SEG SEGMENT
    ASSUME CS:CODE_SEG, DS:CODE_SEG, ES:CODE_SEG, SS:CODE_SEG
SUB_DISPLAY PROC NEAR
    JMP GO
    ALL_DK DB "Suresh Srivastava. $"
GO: MOV DX, OFFSET ALL_OK
    MOV AH, 9
    INT 21H
    RET
SUB_DISPLAY ENDP
CODE_SEG ENDS
    END
```

We can see here both the files are in code segment. END START and ORG statements are only in MAIN.ASM. Because it can have only one entry and we want both files one after another in memory.

# 17.2.1 Memory Models

We have different memory models – tiny, small, medium, compact, huge which set the limit of code and data area. So we select the memory model depending on our program requirements. Different models and their limit for code, data and array are as given below-

|  | Code Segment | Data Segment | Array |
|---|---|---|---|
| Tiny | All in same segment |  |  |
| Small | < 64 K | < 64 K | < 64 K |
| Medium | > 64 K | < 64 K | < 64 K |
| Compact | < 64 K | > 64 K | < 64 K |
| Large | > 64 K | > 64 K | < 64 K |
| Huge | > 64 K | > 64 K | > 64 K |

# 17.2.2 C And Segments in Library

We can link assembly program with C program only when both of them have same segment name. C standard library uses different segment names based on their memory models. To overcome this problem, we have simplified segment directive which is supported by turbo C as well as Microsoft C. We have following keywords for declaration.

+   - `.CODE` - code
+   - `.DATA` - initialized data
+   - `.DATA?` - Uninitialized data
+   - `.FARDATA` - Initialized non-Dgroup data(Compact/Large/Huge)