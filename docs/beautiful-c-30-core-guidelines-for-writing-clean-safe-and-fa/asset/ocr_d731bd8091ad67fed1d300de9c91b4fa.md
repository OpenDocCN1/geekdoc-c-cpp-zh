# Backward compatibility of C++

It’s important to remember where this language came from, and also what motivates its development. There is code in my current project that I wrote in 2005. It looks a little peculiar to today’s programmers as it uses long-discarded paradigms, no auto, no lambdas: it’s a history lesson in source.

However, it still works. It still compiles and runs well. During your career, you will come across code of various ages. It’s important to make use of the latest stand-ard and build with the latest compiler you can find, but it’s also important to know where the language came from and to plan for the future.

> *Stability over decades is a feature.*

Sometimes it isn’t possible to use the latest version of the standard. In embed-ded development, regulation, certification of systems, or elderly infrastructure may force you to use C++11, or even C++98. C++ relies on backward compatibility. It is backward-compatible with C. It is backward-compatible with prior standards. Sta-bility over decades is a feature. This is one of its great strengths: billions of lines of code around the world still build with a modern compiler, occasionally with a little tweaking. At some point you may be asked to maintain this code.

# Forward compatibility and “Y2K”

Conversely, write code that is built to last. At the end of the last century, a problem was unearthed in much of the world’s elderly computer software: only two digits were used to represent the year.⁶ Memory was at a premium, and the efficient thing to do was simply store 74 rather than 1974. The developer thought nothing of it: “This piece of software will not be running in 25 years; surely it will have been replaced.”

6. https://www.britannica.com/technology/Y2K-bug

Ah, such pessimism, or perhaps optimism, depending on your point of view. Of course, once the date rolled around to the year 2000, then the year was represented as 00, spoiling time interval calculations, interest payment calculations, indeed, ANYTHING to do with the passage of time.