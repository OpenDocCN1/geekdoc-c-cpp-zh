
146

Chapter 3. The Processor

```
movl $2, %edx
movl $1, %esi
movl $.LCO, %edi
xor %eax, %eax
call printf
ret
```

The instructions are specified using mnemonics in the main block, which begins at line 9. The earlier lines are assembler directives. The syntax for the directives can vary considerably between different assemblers.

The first line, which gives the name of the file, is a directive. The second line asks the compiler to begin a section called .mydata. One has to dig through the GAS documentation to decipher the portion that follows. The second line states that the section is meant to hold data, each character is one byte, and the strings will be terminated by 0. The strings are terminated by 0, anticipating the need to call the printf function in the C library. In C, strings are always NULL or terminated.

.LCO is the name of the string specified in line 4. It corresponds to a location in memory. Here the assembler takes on the responsibility of storing the specified string in the data section and gives the name .LCO.

The text section, which is not named, begins on line 5. The text section contains instructions. The name main is specified to be a global, and the name of a function in lines 6 and 7—will be outside the file and is the name for address in the text segment, which corresponds to line 8.

In the following code, the 32-bit registers %esi, %edx, and %ecx are filled with 1, 2, and 3, respectively. These are the second, third, and fourth arguments in the call to printf. Thus, the movl instruction is used to move it into the register %edi. The edi is 32 bits. The xor instruction zeros the eax register as a precaution.

The 64-bit x86 architecture requires the first arguments to be placed in %edi, %esi, %edx, and %ecx. The call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

To assemble,⁸ may use

⁸⁸ icc compiler uses the GNU Assembler (GAS). For its documentation, see (Using as, D. Elsner and J. Fenason).

*

# 3.1. Overview of the x86 architecture

```
icc -c addtwo.s
```

to produce the object file addtwo.o (we are back to using icc). The object file can be linked to produce an executable using

```
icc -o addtwo.exe addtwo.o
```

The icc linker takes care of resolving the reference to printf in addtwo.o. When the executable addtwo.exe is run, we are told that

The sum of 1 and 2 is 3

# More about function calls

The output of the next listing, which is

The sum of 1 2 3 4 5 6 7 8 is 36

is hardly more exciting. However, it illustrates function calls made after placing arguments on the stack.

```
1 .file "addmany.s"
2 .section .mydata,"AMS",@probits,1
3 .LCO:
4 .string "The sum of %d %d %d %d %d %d %d %d is %d \n"
5 .text
6 .globl main
7 .type main, @function
8 main:
9 subq $32, %rsp
10 movl $36, 24(%rsp)
11 movl $8, 16(%rsp)
12 movl $7, 8(%rsp)
13 movl $6, (%rsp)
14 movl $5, %r9d
15 movl $3, %ecx
16 movl $2, %edx
17 movl $1, %esi
```

# Chapter 3. The Processor

| | | |
|---|---|---|
| rsp | | |
| | 36 | ← 24(%rsp) |
| | 8 | ← 16(%rsp) |
| | 7 | ← 8(%rsp) |
| | 6 | ← (%rsp) |

Figure 3.3: The stack pointer is moved downward by 32 and the numbers 6, 7, 8, and 36 are placed on the stack before a call to printf. The labeling on the right assumes that the stack pointer has moved downward.

```
movl $LCO, %edi
xor %eax, %eax
call printf
addq $32, %rsp
ret
```

The addmy. program calls printf (on line 21) with a total of 10 arguments. These are the first format string, next the numbers 1 through 8, and finally their, which is 36. The last four of these arguments are pushed onto the stack (see figure 3.3) and the first six are placed in registers as before. It helps to think of the registers as an extension of the stack.

Each argument pushed onto the stack is an int and therefore 4 bytes. Thus, we would need 16 bytes on the stack. However, in 64-bit x86 architecture, each entry on the stack must be a multiple of 8. Therefore, we need 32 bytes on the stack.

By convention, %rsp is the pointer to the top of the stack. On line 9, the pointer %rsp is decremented by 32 bytes to make room for more entries. In x86, the stack grows downward from a high address as shown in figure 3.3. The arguments are pushed onto the stack in reverse order. Thus, the final argument 3 is pushed first onto the stack (line 10). That is followed by the three arguments 8, 7, and 6 (lines 11, 12, and 13, respectively). For addressing modes of the type (%rsp) and 8(%rsp), see figure 3.3. They are explained in greater detail below. The stack pointer

# 3.1. Overview of the x86 architecture

%rsp points to the top, which is 6 (see the right part of figure 3.3).

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

150

Chapter 3. The Processor

the caveat about +8 being +8. In assembly, +8 is always +8.

Wait, theThese are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

173

Wait, theThese

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theWe think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

# 3.1.3 The Stamp Counter

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

We may think of the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack. These are %r9, %r8, %rcx (or %ecx), %rdx (or %edx), %rsi (or %esi), and %rdi (or %edi), in top to order (lines 14 through 19). Thus, the call to printf is made with those arguments. Here printf is an externally defined name and has to be resolved during linking.

Wait, theThese are the registers used to pass arguments as an extension of the stack.
