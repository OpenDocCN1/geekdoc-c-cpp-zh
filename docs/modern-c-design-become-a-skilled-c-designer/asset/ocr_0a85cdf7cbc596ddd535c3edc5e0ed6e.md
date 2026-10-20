#define DECLSPEC #endif

declspec(export)

declspec(import) The declaration of a function foo() that we want to export from our DLL would be written as #include "Declspec.h" DECLSPEC void foo();

When the DLL is built, the preprocessor macro BUILDING_DLL is defined; therefore, the DECLSPEC macro expands to declspec(export). When the DLL is used, the BUILDING_DLL macro is left undefined, and the DECLSPEC macro expands to declspec(import) . Any function or class not decorated with the DECLSPEC macro remains private to the DLL. GCC implements a similar mechanism using a slightly different syntax.

Most Windows programmers are very familiar with the DLL hiding mechanism for controlling module interfaces because globally hiding symbols in DLLs is the