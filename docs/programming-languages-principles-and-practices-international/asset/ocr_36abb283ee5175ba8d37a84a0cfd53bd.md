# 1.2.5 Control: Structured Abstractions

Structured control abstractions divide a program into groups of instructions that are nested within tests that govern their execution. They, thus, help the programmer to express the logic of the primary control structures of sequencing, selection, and iteration (loops). At the machine level, the processor executes a sequence of instructions simply by advancing a program counter through the instructions’ memory addresses. Selection and iteration are accomplished by the use of **branch instructions** to memory locations other than the next one. To illustrate these ideas, Figure 1.4 shows an LC-3 assembly language code segment that computes the sum of the absolute values of 10 integers in an array named LIST. Comments have been added to aid the reader.

```
```asm
        LEA   R1, LIST       ; Load the base address of the array (the first cell)
        AND   R2, R2, #0      ; Set the sum to 0
        AND   R3, R3, #0      ; Set the counter to 10 (to count down)
        ADD   R3, R3, #10
WHILE   LDR   R4, R1, #0      ; Top of the loop: load the datum from the current
                              ; array cell
        BRZP  INC             ; If it’s >= 0, skip next two steps
        NOT   R4, R4          ; It was < 0, so negate it using twos complement
                              ; operations
        ADD   R4, R4, #1
INC     ADD   R2, R2, R4      ; Increment the sum
        ADD   R1, R1, #1      ; Increment the address to move to the next array
                              ; cell
        ADD   R3, R3, #-1     ; Decrement the counter
        BRP   WHILE           ; Goto the top of the loop if the counter > 0
        ST    R2, SUM         ; Store the sum in memory
```
```

**Figure 1.4** An array-based loop in assembly language

If the comments were not included, even a competent LC-3 programmer probably would not be able to tell at a glance what this algorithm does. Compare this assembly language code with the use of the structured if and for statements in the functionally equivalent C++ or Java code in Figure 1.5.

```
```cpp
int sum = 0;
for (int i = 0; i < 10; i++){
    int data = list[i];
    if (data < 0)
        data = -data;
    sum += data;
}
```
```

**Figure 1.5** An array-based loop in C++ or Java

Structured selection and loop mechanisms are studied in Chapter 9.