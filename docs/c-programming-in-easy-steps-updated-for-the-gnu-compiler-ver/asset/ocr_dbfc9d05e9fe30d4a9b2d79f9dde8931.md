...cont'd

+   1. Make a copy of the previous example, lotto.c, and rename it as winlotto.c
+   2. At the start of the renamed program file, insert a further preprocessor instruction to make the WINAPI available
+      `#include <windows.h>`
+   3. Next, replace the line containing `int main()` with the one that communicates with the Windows operating system
+      `int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)`
+   4. Now, replace the call to `printf()` that outputs the selected numbers with a call that displays them in a dialog box
+      `MessageBox(NULL, str, "Lotto Number Picker", MB_OK | MB_ICONEXCLAMATION);`
+   5. Save the program file, compile the program using the special compiler option, then run the program – both from the command line and by a double-click

![](bbox=[0.7, 0.1, 0.85, 0.25])

![](bbox=[0.05, 0.67, 0.7, 0.97])

![](bbox=[0.75, 0.62, 0.95, 0.85])

![](bbox=[0.75, 0.8, 0.98, 0.98])