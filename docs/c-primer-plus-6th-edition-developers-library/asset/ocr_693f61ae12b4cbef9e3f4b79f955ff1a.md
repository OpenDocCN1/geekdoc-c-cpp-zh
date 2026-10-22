Including a large header file doesn’t necessarily add much to the size of your program. The content of header files, for the most part, is information used by the compiler to generate the final code, not material to be added to the final code.

# Header Files: An Example

Suppose you developed a structure for holding a person’s name and also wrote some functions for using the structure. You could gather together the various declarations in a header file. Listing 16.6 shows an example of this.

# Listing 16.6 The names_st.h Header File

```
// names_st.h -- names_st structure header file
// constants
#include <string.h>
#define SLEN 32

// structure declarations
struct names_st
{
    char first[SLEN];
    char last[SLEN];
};

// typedefs
typedef struct names_st names;

// function prototypes
void get_names(names *);
void show_names(const names *);
char * s_gets(char * st, int n);
```

This header file includes many of the kinds of things commonly found in header files: #define directives, structure declarations, typedef statements, and function prototypes. Note that none of these things are executable code; rather, they are information that the compiler uses when it creates executable code.

This particular header file is a bit naïve. Normally, you should use #ifndef and #define to protect against multiple inclusions of a header file. We’ll return to that technique later.

Executable code normally goes into a source code file, not a header file. For example, Listing 16.7 shows the function definitions for those functions prototyped in the header file. It includes the header file so that the compiler will know about names type.