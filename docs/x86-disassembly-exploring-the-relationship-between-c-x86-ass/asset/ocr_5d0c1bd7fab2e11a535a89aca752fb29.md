# Disassembler Issues

dissy

This program is a interactive disassembler that uses objdump.

```
http://code.google.com/p/dissy/
```

x86dis

This program can be used to display binary streams such as the boot sector or other unstructured binary files.

ldasm

LDasm (Linux Disassembler) is a Perl/Tk-based GUI for objdump/binutils that tries to imitate the 'look and feel' of W32Dasm. It searches for cross-references (e.g. strings), converts the code from GAS to a MASM-like style, traces programs and much more. Comes with PTrace, a process-logger.

```
http://www.feedface.com/projects/ldasm.html
```

# ## 2.3 Disassembler Issues

As we have alluded before, there are a number of issues and difficulties associated with the disassembly process. The two most important difficulties are the division between code and data, and the loss of text information.

# ### 2.3.1 Separating Code from Data

Since data and instructions are all stored in an executable as binary data, the obvious question arises: how can a disassembler tell code from data? Is any given byte a variable, or part of an instruction?

The problem wouldn't be as difficult if data were limited to the .data section of an executable (explained in a later chapter) and if executable code were limited to the .code section of an executable, but this is often not the case. Data may be inserted directly into the code section (e.g. jump address tables, constant strings), and executable code may be stored in the data section (although many new systems are preventing this for security reasons).

Many interactive disassemblers will give the user the option to render segments of either code or data, but non-interactive disassemblers will make the separation automatically. Disassemblers often provide the instruction AND for the corresponding hex data on the same line, to reduce the need for decisions to be made about the nature of the code. Some disassemblers allow you to specify rules about what to disassemble or label names, based on the content of the object under scrutiny. Scripting your own 'crawler' in this way is more efficient; for large programs interactive disassembling may be impractical to the point of being infeasible.

The general problem of separating code from data in arbitrary executable programs is equivalent to the halting problem. As a consequence, it is not possible to write a disassembler that will correctly separate code and data for all possible input programs. Reverse engineering