**Document extremely short names with translation tables in the code**  In languages that allow only very short names, include a translation table to provide a reminder of the mnemonic content of the variables. Include the table as comments at the beginning of a block of code. Here’s an example:

```
**Fortran Example of a Good Translation Table**

C *****************************************************************
C    Translation Table
C
C    Variable    Meaning
C
C    XPOS        x-Coordinate Position (in meters)
C    YPOS        Y-Coordinate Position (in meters)
C    NDSCMP      Needs Computing (=0 if no computation is needed;
C                              =1 if computation is needed)
C
C    PTGTTL      Point Grand Total
C    PTVLMX      Point Value Maximum
C    PSCRMX      Possible Score Maximum
C *****************************************************************
```

You might think that this technique is outdated, but as recently as mid-2003 I worked with a client that had hundreds of thousands of lines of code written in RPG that was subject to a 6-character-variable-name limitation. These issues still come up from time to time.

**Document all abbreviations in a project-level “Standard Abbreviations” document**
Abbreviations in code create two general risks:

+   - A reader of the code might not understand the abbreviation.
+   - Other programmers might use multiple abbreviations to refer to the same word, which creates needless confusion.

To address both these potential problems, you can create a “Standard Abbreviations” document that captures all the coding abbreviations used on your project. The document can be a word processor document or a spreadsheet. On a very large project, it could be a database. The document is checked into version control and checked out any time one creates a new abbreviation in the code. Entries in the document should be sorted by the full word, not the abbreviation.

This might seem like a lot of overhead, but aside from a small amount of startup overhead, it really just sets up a mechanism that helps the project use abbreviations effectively. It enables the first of the two general risks described above by documenting all abbreviations in use. The fact that a programmer can’t create a new abbreviation without the overhead of checking the Standard Abbreviations document out of ver-