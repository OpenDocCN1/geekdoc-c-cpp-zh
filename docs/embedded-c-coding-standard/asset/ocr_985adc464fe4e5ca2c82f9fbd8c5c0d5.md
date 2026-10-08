Embedded C Coding Standard

# 3.6 Non-Printing Characters

Rules:

+   a. Whenever possible, all source code lines shall end only with the single character 'LF' (ASCII 0x0A), not with the pair 'CR'-'LF' (0x0D 0x0A).
b. The only other non-printable character permitted in a source code file is the form feed character 'FF' (ASCII 0x0C).

**Example:** It's not possible to demonstrate non-printing characters in print.

**Reasoning:** The multi-character sequence 'CR'-'LF' is more likely to cause problems in a multi-platform development environment than the single character 'LF'. One such problem is associated with multi-line preprocessor macros on Unix platforms.

**Enforcement:** Whenever possible, programmer's editors shall be configured to use LF. In addition, an automated tool shall scan all new or modified source code files during each build, replacing each CR-LF sequence with an LF.