| ATTRIBUTE | AUTO | EXTERN | STATIC EXTERN | STATIC INTERN | REGISTER |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Retain value upon leaving block | NO | YES | YES | YES | NO |
| Available to multiple functions | NO | YES | YES | NO | NO |
| Available to other source files | NO | YES | NO | NO | NO |
| Zero default when not initialized | NO | YES | YES | YES | NO |
| Initialized once at compile time | NO | YES | YES | YES | NO |
| Initialize arrays and structures | NO | YES | YES | YES | NO |
| Variables in machine registers | NO | NO | NO | NO | YES |