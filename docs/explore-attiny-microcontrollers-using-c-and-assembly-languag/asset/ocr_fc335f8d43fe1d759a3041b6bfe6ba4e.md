```
.ORG 0
```

An example of an assembler directive with a label and a single operand is the BYTE directive, shown below, which is also covered in the next section.

```
count: .BYTE 1
```

# 9.3.1 Specifying Code and Data Locations

The AVRASM2 Assembler program supports a combination of directives that allow code and data to be placed at the desired addresses and in the specified memory type. These are the ORG, CSEG, DSEG and ESEG directives, described further in the subsections that follow.

# 9.3.1.1 ORG Assembler Directive

ORG is an assembler directive that is short for *origin* and is used to set the program origin or start address of a section of memory. ORG can be written in upper case or lower case letters, but must start with a dot when used in a program. .ORG and .org both work. The simple code snippet below shows how ORG can be used to set the program’s start address.

```
.ORG 0
sbi DDRB, DDB4    ; LED on pin PB4
sbi PORTB, PORTB4 ; Switch LED on
loop:
rjmp loop         ; Infinite loop
```

In the code snippet .ORG is set to 0 which sets the start address of the program code to 0. Code is placed at address 0 by default, which is why none of the programs so far have needed to use the ORG directive.

As another example, we can put our code at address 0x40, leaving the Flash memory above it free. We do need to put an RJMP instruction at address 0 that jumps to our program code at address 0x40 because at reset, code starts executing at address 0. The following code snippet shows how this is done.