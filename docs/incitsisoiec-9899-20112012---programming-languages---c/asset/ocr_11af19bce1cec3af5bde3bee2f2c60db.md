# 7.31.9 Boolean type and values <stdbool.h>

The undefined and potentially redefines makes bool, true, and false an obsolete feature.

# 7.31.10 Integer types <stdint.h>

Typedef names beginning with int and uint and ending with _t may be added to the types defined in the <stdint.h> header. Macro names beginning with INT, UINT and ending with _MAX, _MIN, or _C may be added to the macros defined in the <stdint.h> header.

# 7.31.11 Input/output <stdio.h>

Lowercase letters may be added to the conversion specifications and length modifiers in printf and fscanf. Other characters may be used in extensions.

The use of unget on a binary stream where the file position indicator is zero prior to the call is an obsolete feature.

# 7.31.12 General utilities <stdlib.h>

Function names beginning with str and a lowercase letter may be added to the declarations in <stdlib.h> header.

# 7.31.13 String handling <string.h>

Function names begin with str, mem, mem or wcs and a lowercase letter may be added to the declarations in the <string.h> header.

# 7.31.14 Date and time <time.h>

Macros beginning with TIME_ and an uppercase letter may be added to the macros in the <time.h> header.

# 7.31.15 Threads <threads.h>

Function names, types and enumeration constants that begin with either cnd_mtx_thrd_ or tss_ and a lowercase letter may be added to the declarations in the <threads.h> header.

# 7.31.16 Extended multibyte and wide character utilities <wchar.h>

Function names that begin with wcs and a lowercase letter may be added to the declarations in the <wchar.h> header.

Lowercase letters may be added to the conversion specifications and length modifiers in fprintf and fscanf. Other characters may be used in extensions.