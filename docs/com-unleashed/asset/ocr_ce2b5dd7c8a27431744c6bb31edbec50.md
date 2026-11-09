# **LISTING 6.22 Continued**

```
```idl
[id(0xfffffe00), propput]
HRESULT _stdcall Color([in] OLE_COLOR Value);
[id(0xfffffe00), propput]
HRESULT _stdcall Color(
    [out, retval] IFontDisp** Value);
[id(0xfffffe00), propputref]
HRESULT _stdcall Font([in] IFontDisp* Value);
[id(0xfffffe00), propputref]
HRESULT _stdcall Font([in] IFontDisp* Value);
[id(0xfffffe00), propputref]
HRESULT _stdcall Font([in] IFontDisp* Value);
[id(0x00000004), propput]
HRESULT _stdcall KeyPreview(
    [out, retval] VARIANT_BOOL* Value);
[id(0x00000004), propput]
HRESULT _stdcall KeyPreview([in] VARIANT_BOOL Value);
[id(0x00000005), propput]
HRESULT _stdcall PixelsPerInch(
    [out, retval] long* Value);
[id(0x00000005), propput]
HRESULT _stdcall PixelsPerInch([in] long Value);
[id(0x00000006), propput]
HRESULT _stdcall PrintScale(
    [out, retval] TxPrintScale* Value);
[id(0x00000006), propput]
HRESULT _stdcall PrintScale([in] TxPrintScale Value);
[id(0x00000007), propput]
HRESULT _stdcall Scaled(
    [out, retval] VARIANT_BOOL* Value);
[id(0x00000007), propput]
HRESULT _stdcall Scaled([in] VARIANT_BOOL Value);
[id(0x00000008), propput]
HRESULT _stdcall Active(
    [out, retval] VARIANT_BOOL* Value);
[id(0x00000009), propput]
HRESULT _stdcall DropTarget(
    [out, retval] VARIANT_BOOL* Value);
[id(0x00000009), propput]
HRESULT _stdcall DropTarget([in] VARIANT_BOOL Value);
[id(0x0000000a), propput]
HRESULT _stdcall HelpFile([out, retval] BSTR* Value);
[id(0x0000000a), propput]
HRESULT _stdcall HelpFile([in] BSTR Value);
[id(0x0000000b), propput]
HRESULT _stdcall WindowState(
    [out, retval] TxWindowState* Value);
[id(0x0000000b), propput]
HRESULT _stdcall WindowState(
    [in] TxWindowState Value);
[id(0xfffffffe), propput]
HRESULT _stdcall Enabled(
```
```