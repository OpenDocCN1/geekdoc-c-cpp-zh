feature before I use, but that is not always possible and everybody reads the text strictly sequentially. I assume some technical maturity from my readers. So, the reader is encouraged to use the cross references and the index.

Similarly, this tour presents the standard libraries in terms of examples, rather than exhaustive. The reader is encouraged to search out additional and supporting material as needed. There is far more in the C++ ecosystem than the facilities offered by ISO standard (e.g., libraries, build systems, tools and development environments). There is an enormous amount of material (varying quality) available on the web. Most readers will find useful tutorial and overview videos from forums as CCpp and Meeting C++. For technical details of the language and library offered by the C++ standard, I recommend [Cpppreference]. For example, if I mention a standard-library function or class, its definition can be easily looked up, and by examining its documentation, many related functions can be found as a layer.

This tour presents C++ as an whole, rather than as a layer. Consequently, I rarely identify features as present in C, C++98, or later standards. Information can be found in... I focus on fundamentals and try to be brief, but I have not completely resisted the temptation to overrepresent novel features, such as modules (§3.2.2), concepts (§8.2), and coroutines (§18.6). Slightly favoring recent developments also seems to satisfy the curiosity of many readers who already know older version of C++.

A programming language manual or simply states what can be done, but that programmers are often more interested in learning how to use the language well. This aspect is already addressed in the selection of topics covered, partly in the text, and specifically in the advice sections. More advice about what constitutes good C++ can be found in the C++ Core Guidelines [Stroustrup,2015]. The Core Guidelines can be a good source for further exploration of the ideas presented in this book. You may note a remarkable similarity of the advice formulation and even the numbering of advice between the Core Guidelines and this book. One reason is that the first edition of A Tour of C++ was a major source of the initial Core Guidelines.

# Acknowledgments

Thanks to all who completed and corrected the early editions of A Tour of C++, especially to the students in my "Design Using C++" course at Columbia University. Thanks to Morgan Stanley for giving me time to write this third edition. Thanks to Chuck Allison, Guy Davidson, Stephen Dewhurst, Kate Gregory, Danny Kalev, Go Nishanov, and J.C. van Winkel for reviewing the book and suggesting many improvements.

This book was set using by the author using macros originating from Brian Kernaghan.

Manhattan, New York

Bjarne Stroustrup