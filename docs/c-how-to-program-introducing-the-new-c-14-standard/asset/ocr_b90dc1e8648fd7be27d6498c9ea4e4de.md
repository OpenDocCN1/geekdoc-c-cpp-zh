# E.6 `#error` and `#pragma`  
Preprocessing Directives

# The `#error` directive

+   - `error` *tokens*

prints an implementation-dependent message including the *tokens* specified in the directive. The tokens are sequences of characters separated by spaces. For example,

```
```text
#error 1 - Out of range error
```
```

contains six tokens. In one popular C++ compiler, for example, when a `#error` directive is processed, the tokens in the directive are displayed as an error message, preprocessing stops and the program does not compile.

# The `#pragma` directive

```
```text
#pragma
```
```