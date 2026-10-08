Embedded C Coding Standard

# 2.2 Locations and Content

Rules:

+   - All comments shall be written in clear and complete sentences, with proper spelling and grammar and appropriate punctuation.

+   - The most useful comments generally precede a block of code that performs one step of a larger algorithm. A blank line shall follow each such code block. The comments in front of the block should be at the same indentation level.

+   - Avoid the obvious. Assume the reader knows the C programming language. For example, end-of-line comments should only be used where the meaning of one line could be unclear from the variable and function names and operations alone where a short comment makes it clear. Specifically, avoid unhelpful and redundant comments, e.g., `number << 2; // Shift number left 2 bits.`

+   - The number and length of individual comment blocks shall be proportional to the complexity of the code they describe.

+   - Whenever an algorithm or technical detail is defined in an external reference—e.g., a design specification, patent, or textbook—a comment should include a sufficient reference to the original source to allow a reader of the code to locate the document.

+   - Whenever a flow chart or other diagram is needed to sufficiently document the code, the drawing should be maintained with the source code under version control and the comments should reference the diagram by file name or title.

+   - All assumptions shall be spelled out in comments.³

+   - Each module and function shall be commented in a manner suitable for automatic documentation generation, e.g., via Doxygen.

![](bbox=[0.793, 0.687, 0.856, 0.743])

> ³ Even better than comments is a set of design-by-contract tests or assertions. See, e.g., barrgroup.com/embedded-systems/how-to/design-by-contract-for-embedded-software.