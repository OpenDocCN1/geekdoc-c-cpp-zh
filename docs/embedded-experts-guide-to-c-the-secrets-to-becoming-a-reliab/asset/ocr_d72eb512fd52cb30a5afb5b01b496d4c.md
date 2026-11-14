# Endnotes for Chapter 2 - Writing Safer C

+   1 I would say that I know a fair bit about the language – I wouldn’t be writing a book about it if I didn’t. But I certainly don’t consider myself an expert; I am regularly discovering new and unexpected things about the language.

+   2 Complete portability is usually desirable but often not possible; there will almost always be some part of the code that relies on a specific implementation to work.

+   3 They are also broadly compatible; although MISRA C is more restrictive than BARR C, BARR C is written with the intent that it does not contradict anything within MISRA C.

+   4 Tokenisation is a stage of the compilation process used to demarcate and classify the individual parts of each C statement so that they can be correctly compiled. In the same way that a sentence can be analysed in terms of nouns, verbs and other syntactic units, a program can be understood in terms of variables, operators, and other coding units.

+   5 In general, preprocessor directives should not be terminated with a semicolon, particularly #define directives. Doing so may not cause issues for the preprocessor itself but is more likely than not to be a programming error.