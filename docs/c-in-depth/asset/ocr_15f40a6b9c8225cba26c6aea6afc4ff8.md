```
.CODE
    ORG 100H
START:
DISPLAY PROC NEAR
    CALL SUB_DISPLAY
INT 20H
DISPLAY ENDP
    END START
```

# EXPROC.ASM

```
PUBLIC SUB_DISPLAY
.MODEL SMALL
.CODE
SUB_DISPLAY PROC NEAR
    JMP GO
    ALL_OK DB "Suresh Srivastava.$"
GO: MOV DX, OFFSET ALL_OK
    MOV AH, 9
    INT 21H
    RET
SUB_DISPLAY ENDP
END
```

Here we can see that SUB_DISPLAY is declared as PUBLIC in file EXPROC.ASM, so that it can be called in another file. It is declared as EXTRN in MAIN.ASM, so it can be called in file MAIN.ASM.

+   d:\>TASM MAIN.ASM
+   d:\>TASM EXPROC.ASM
+   d:\>TLINK MAIN+EXPROC
+   d:\>EXE2BIN MAIN MAIN.COM
+   d:\>MAIN

Suresh Srivastava

# 17.3 Linking Assembly Procedure in C Program

Now we will see how we can call one assembly procedure in C program. We will write main program in C, which will call assembly procedure from asm program for getting the scan code of any key of keyboard.

# Main.c

```
extern int getscancode( );
main()
{
```