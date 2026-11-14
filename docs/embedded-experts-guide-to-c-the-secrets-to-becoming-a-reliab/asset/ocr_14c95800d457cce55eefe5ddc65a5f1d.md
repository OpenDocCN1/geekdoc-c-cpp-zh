# Endnotes for Chapter 11 - Bootloaders and Operating Systems

1 That is not to say an embedded OS cannot be maintained; however, they rarely rely upon the in-situ update model used by more familiar operating systems and may be required to work for years without modification to the code.

2 In principle, there is nothing wrong with self-modifying code, which has been in use for decades. However, if the code makes a breaking change to itself or an error occurs during modification, it becomes unusable. A bootloader cannot entirely prevent this from happening, but it can be designed to detect errors in the code or provide fail-safe fallback routines if runtime errors should occur.

3 This information could be omitted, but doing so requires a bootloader which copies a fixed number of words into program memory, therefore placing additional restrictions on the program to be loaded as well as how it is stored and potentially the layout of memory once it has been loaded as well.

4 The suggested function declaration given in the C Standard is int main(int arg, char However, the standard allows this to be substituted for either an equivalent declaration (usually int main(int arg, char ** argv)) or for “some other implementation defined” declaration. In other words, any declaration is allowed for the function, but it is dictated by the compiler, not the programmer. The