Embedded C Coding Standard

# 1.7 Keywords to Avoid

Rules:

+   a. The auto keyword shall not be used.

+   b. The register keyword shall not be used.

+   c. It is a preferred practice to avoid all use of the goto keyword. If goto is used it shall only jump to a label declared later in the same or an enclosing block.

+   d. It is a preferred practice to avoid all use of the continue keyword.

Reasoning: The auto keyword is an unnecessary historical feature of the language. The register keyword presumes the programmer is smarter than the compiler. There is no compelling reason to use either of these keywords in modern programming practice.

The keywords goto and continue still serve purposes in the language, but their use too often results in spaghetti code. In particular, the use of goto to make jumps orthogonal to the ordinary control flows of the structured programming paradigm is problematic. The occasional use of goto to handle an exceptional circumstance is acceptable if it simplifies and clarifies the code.

Enforcement: The presence of forbidden keywords in new or modified source code shall be detected and reported via an automated tool at each build. To the extent that the use of goto or continue is permitted, code reviewers should investigate alternative code structures to improve code maintainability and readability.