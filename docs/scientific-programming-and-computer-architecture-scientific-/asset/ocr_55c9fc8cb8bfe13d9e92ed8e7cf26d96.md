# 2.3. Building programs using GNU Make

| $@ | Target |
| --- | --- |
| $< | The first prerequisite |
| $\$ | Prerequisites newer than the target |
| $\$^ | All prerequisites with duplicates eliminated |
| $+ | All prerequisites including duplicates |

Table 2.2: Automatic variables recognized by the make utility.

list of all prerequisites of the target. If a dependency leibniz.exe: xyz.o is given elsewhere in the Makefile, xyz.o will be in $\$ as well. The three most important automatic variables are $@, $\$$, and $<.

Pattern rules form the section of the makevars.mk file at the root of the source tree (see figure 2.2 for the section tree).

11 .SUFFIXES: 
12 .SUFFIXES: .cpp .o .exe .s d
13 %o: %.cpp
14     $ $(CFLAGS) -c $$
15 %s: %.cpp
16     $ $(CFLAGS) -fno-verbose-asm -S $$
17 %o: %s
18     $ $(CFLAGS) -c $$
19 %.exe: %o
20     $ $(CPP) -o $$ $(filter %o,$^) $(LIBS)

Line 11 is a rule with .SUFFIXES as the target and an empty list of prerequisites. If has the effect of deleting many suffixes and pattern rules ordered by GNU make by default. The rule on line 16 specifies the suffixes we want to use in pattern rules that are explicitly given later.

The rule on lines 13 and 14 is the pattern rule for generating an object file from a C++ source with the file extension .cpp. The pattern in the dependency is as follows:

%.o: %.cpp

It matches a dependency such as

```
Aitken.o: Aitken.cpp Aitken.hh
```