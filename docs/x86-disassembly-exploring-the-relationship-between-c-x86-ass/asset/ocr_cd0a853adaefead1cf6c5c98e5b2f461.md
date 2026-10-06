# Assemblers and Compilers

# 1.3 Intel Syntax Assemblers

Because of the pervasiveness of Intel-based IA-32 microprocessors in the home PC market, the majority of assembly work done (and the majority of assembly work considered in this wikbook) is x86-based. Many of these assemblers (or new versions of them) can handle amd64/x86_64/EMT64 code well, although this wikbook will focus primarily on 32 bit (x86/IA-32) code examples.

# 1.3.1 MASM

MASM is Microsoft's assembler, an abbreviation for 'Macro Assembler.' However, many people use it as an acronym for 'Microsoft Assembler,' and the difference isn't a problem at all. MASM has a powerful macro feature, and is capable of writing very low-level syntax, and pseudo-high-level code with its macro feature. MASM 6.15 is currently available as a free-download from Microsoft, and MASM 7.xx is currently available as part of the Microsoft platform DDK.

+   * MASM uses Intel Syntax.
* MASM is used by Microsoft to implement some low-level portions of its Windows Operating systems.
* MASM, contrary to popular belief, has been in constant development since 1980, and is upgraded on a needs-basis.
* MASM has always been made compatible by Microsoft to the current platform, and executable file types.
* MASM currently supports all Intel instruction sets, including SSE2.

Many users love MASM, but many still dislike the fact that it isn't portable to other systems.

# 1.3.2 TASM

TASM, Borland's 'Turbo Assembler,' is a functional assembler from Borland that integrates seamlessly with Borland's other software development tools. Current release version is 5.0. TASM syntax is very similar to MASM, although it has an 'IDEAL' mode that many users prefer. TASM is not free.

# 1.3.3 NASM

NAS, the 'Net Assembler,' is a free, portable, and retargetable assembler that works on both Windows and Linux. It supports a variety of Windows and Linux executable file formats, and outputs pure binary. NASM is not as 'mature' as either MASM or TASM, but is:

+   * more portable than MASM
* cheaper than TASM
* strives to be very user-friendly