```
DISPLAY ENDP
    END START
```

Here our program has procedure to print the string. Let us take another program that calls procedure, which is used to display the string.

```
CODE_SEG SEGMENT
    ASSUME CS:CODE_SEG, DS:CODE_SEG, ES:CODE_SEG, SS:CODE_SEG
    ORG 100H

START: DISPLAY PROC NEAR
    CALL SUB_DISPLAY
    INT 20H
DISPLAY ENDP
SUB_DISPLAY PROC NEAR
    JMP GO
    ALL_OK DB "Suresh Srivastava. $"
GO: MOV DX, OFFSET ALL_OK
    MOV AH, 9
    INT 21H
    RET
SUB_DISPLAY ENDP
CODE_SEG ENDS
    END START
```

Now think about modular programming. Suppose we want to write all the procedures in different files and those procedures will be called in the main module. So we will have to link all the files. Let us take an example program that has two files, one file has procedure which is called in another file.

# MAIN.ASM

```
CODE_SEG SEGMENT
    ASSUME CS:CODE_SEG, DS:CODE_SEG, ES:CODE_SEG, SS:CODE_SEG
    ORG 100H

START:
DISPLAY PROC NEAR
    CALL SUB_DISPLAY
    INT 20H
DISPLAY ENDP
CODE_SEG ENDS
    END START
```