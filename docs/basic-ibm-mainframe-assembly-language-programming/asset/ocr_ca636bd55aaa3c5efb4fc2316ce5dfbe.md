# 18. CSECTS, DSECTS and Base Registers

# 18.1 CSECT

Assembly language programs are comprised of one or more sections. There are three types of sections: control sections (CSECTs), common sections (COMs) and dummy sections (DSECTs). CSECTs contain ordinary code, dummy sections do not generate object code but are layouts or mappings of memory, and common sections are areas of memory common to multiple object modules.

A CSECT directive is used to begin or continue a control section. The label on the CSECT directive is the name of the section for linkage purposes. The START directive, used only at the beginning of an assembly program, is the equivalent of a CSECT. In a program with multiple CSECTs, the code for several sections may be intermingled in the source file. The CSECT directive is used to identify to which section different code sections belong.

```
FIRST     CSECT
          .
          .                 some code for CSECT FIRST
          .
SECOND    CSECT
          .
          .                 some code for CSECT SECOND
          .
TMPLT1    DSECT
          .
          .                 some code for DSECT TMPLT1
          .
FIRST     CSECT
          .
          .                 more code for CSECT FIRST
          .
SECOND    CSECT
          .
          .                 more code for CSECT SECOND
          .
```

Figure 60 CSECT/DSECT Flow

In an assembly language program you may have several CSECTS and DSECTS (discussed below). These need not be contiguous. You may begin a CSECT and write some code then begin another, likewise write some code, interrupt that one and declare a DSECT, and then resume coding a previous CSECT. The