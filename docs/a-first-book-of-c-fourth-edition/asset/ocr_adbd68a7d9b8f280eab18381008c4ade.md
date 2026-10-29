| Element | String array | Expression | Value |
|---|---|---|---|
| Zeroth element | t | string2[0] != '\0' | 1 |
| First element | h | string2[1] != '\0' | 1 |
| Second element | i | string2[2] != '\0' | 1 |
|  | s |  |  |
|  |  |  |  |
|  | i |  |  |
|  | s |  |  |
| . |  | . | . |
| . | a | . | . |
| . |  | . | . |
|  | s |  |  |
|  | t |  |  |
|  | r |  |  |
|  | i |  |  |
|  | n |  |  |
| Fifteenth element | g | string2[15] != '\0' | 1 |
| Sixteenth element | \0 | string2[16] != '\0' | 0 |
| End-of-string marker |  |  |  |

Figure 15.3 The while test becomes false at the end of the string