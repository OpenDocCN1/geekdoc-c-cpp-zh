# WHERE ARE THE FILES?

A C programming project needs more than just the source code: It includes header files and libraries. The header files are called in by using the #include directives; libraries are brought in by the linker. Don't worry about these files, because the compiler and linker handle the details for you.

Because C comes from a Unix background, traditional locations for the header and library files are used. Header files are found in the /usr/include directory (folder). The library files dwell in the /usr/lib directory. Those are system folders, so look but don't touch the contents. I frequently peruse header files to look for hints or information that may not be obvious from the C language documentation. (Header files are plain text; library files are data.)

If you're using a Unix-like operating system, you can visit those directories and peruse the multitude of files located there. On a Windows system, the files are kept with the compiler, usually, in include and lib folders relative to the compiler's location.