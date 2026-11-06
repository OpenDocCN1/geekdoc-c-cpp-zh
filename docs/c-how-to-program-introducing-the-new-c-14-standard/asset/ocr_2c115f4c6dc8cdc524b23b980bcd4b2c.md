# 6.10 Scope Rules

The portion of a program where an identifier can be used is known as its *scope*. For example, when we declare a local variable in a block, it can be referenced only in that block and in blocks nested within that block. This section discusses **block scope** and **global namespace scope**. Later we’ll see other scopes, including **class scope** in **Chapter 9**, and **function scope**, **function-prototype scope** and **namespace scope** in **Chapter 23**.

# Block Scope

Identifiers declared *inside* a block have block scope, which begins at the identifier’s declaration and ends at the terminating right brace (`}`) of the enclosing block. Local variables have block scope, as do function parameters (even though they’re declared outside the block’s braces). Any block can contain variable declarations. When blocks are nested and an identifier in an outer block has the same name as an identifier in an inner block, the one in the outer block is “hidden” until the inner block terminates—the inner block “sees” its own local variable’s value and not that of the enclosing block’s identically named variable.

![](bbox=[0.12, 0.825, 0.195, 0.876])

# Common Programming Error 6.6