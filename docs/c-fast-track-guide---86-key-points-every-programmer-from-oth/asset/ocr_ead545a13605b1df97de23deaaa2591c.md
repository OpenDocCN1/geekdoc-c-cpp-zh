DllImport tells the C# compiler to link a method with a native DLL function.

user32.dll is a Windows system DLL that contains GUI-related functions.

MessageBox is a simple function from that DLL that creates a pop-up message box.

IntPtr.Zero is used to indicate no owner window.

The CharSet option ensures correct string marshaling between C# and native code.

The uint type parameter specifies the type of message box (e.g., with OK/Cancel, icons, etc.).

P/Invoke is powerful but must be used carefully: incorrect parameter types or unmanaged resources can cause crashes or memory leaks.

Ideal when dealing with legacy code, hardware access, or OS-level functionality.

# [Supplement]

You can also use P/Invoke to call C functions in your own compiled DLLs, not just system DLLs.

Tools like DllImport Generator and PInvoke.net help you find signatures.

You must ensure correct data types and memory layout—managed and unmanaged code handle memory differently.

P/Invoke is part of .NET’s broader native interop features, including COM and unsafe code.