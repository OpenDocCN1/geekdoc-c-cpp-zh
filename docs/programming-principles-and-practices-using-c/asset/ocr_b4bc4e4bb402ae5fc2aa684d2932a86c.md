+   - Who wrote this code and when
- Version numbers
- What complicated code fragments are supposed to do
- What the general design ideas are
- How the source code is organized
- What assumptions are made about inputs
- What parts of the code are still missing and what cases are still not handled

+   - Use meaningful names.
	- That doesn’t simply mean “Use long names.”
- Use a consistent layout of code.
	- Your IDE tries to help, but it can’t do everything and you are the one responsible.
	- The style used in this book is a reasonable starting point.
- Break code into small functions, each expressing a logical action.
	- Try to avoid functions longer than a page or two; most functions will be much shorter.
- Avoid complicated code sequences.
	- Try to avoid nested loops, nested if-statements, complicated conditions, etc. Unfortunately, you sometimes need those, but remember that complicated code is where bugs can most easily hide.
- Use library facilities rather than your own code when you can.
	- A library is likely to be better thought out and better tested than what you could produce as an alternative while busily solving your main problem.

This is pretty abstract just now, but we’ll show you example after example as we go along.

Get the program to compile. Obviously, your compiler is your best help here. Its error messages are usually helpful – even if we always wish for better ones – and, unless you are a real expert, assume that the compiler is always right; if you are a real expert, this book wasn’t written for you. Occasionally, you will feel that the rules the compiler enforces are stupid and unnecessary (they rarely are) and that things could and ought to be simpler (indeed, but they are not). However,