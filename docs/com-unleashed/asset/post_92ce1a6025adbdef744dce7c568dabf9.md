
Both the VB and ATL projects for this experiment are available on the CD-ROM in the Chapter06 directory, in a subdirectory named vbsink.

## How Different Tools Implement Events

The next two sections are experiments that I believe are most useful in understanding how COM events work. These experiments show how different compilers generate their own event interfaces.

### Events and Visual Basic

If you create a VB ActiveX control and compile the project into an OCX, you can use OLEView to read the OCX’s type library. Start OLEView and select File, View TypeLib from the menu bar. Select your newly created OCX and click the Open button. The right pane of the ITypeLib viewer displays the content of the type library in IDL format. Listing 6.21 is the default IDL generated for a Visual Basic ActiveX control.

**Listing 6.21** IDL of Visual Basic ActiveX Control

```idl
// Generated .IDL file (by the OLE/COM Object Viewer)
//
// typelib filename: Project1.ocx
// Forward declare all types defined in this typelib
interface _UserControl1;
dispinterface __UserControl1;

[
    uuid(700B9D89-8D5F-11D2-9C2B-DC6F06C10000),
    version(1.0),
    helpstring("Project1")
]
library Project1
{
    // TLib : OLE Automation :
    // {00020430-0000-0000-C000-000000000046}
    importlib("STDOLE2.TLB");

    [
        odl,
        uuid(700B9B86-8D5F-11D2-9C2B-DC6F06C10000),
        version(1.0),
        hidden,
        dual,
        nonextensible,
        oleautomation
    ]
    interface _UserControl1 : IDispatch {
    };

    [
        uuid(700B9DB7-8D5F-11D2-9C2B-DC6F06C01000),
        version(1.0),
        noncreatable,
        control
    ]
    coclass UserControl1 {
        [default] interface _UserControl1;
        [default, source] dispinterface __UserControl1;
    };

    [
        uuid(700B9DB8-8D5F-11D2-9C2B-DC6F06C01000),
        version(1.0),
        hidden,
        nonextensible
    ]
    dispinterface __UserControl1 {
        properties:
        methods:
    };
};
```

Note that the control implements two interfaces, one dual interface and one dispatch interface. The dual interface contains the properties and methods of the ActiveX object. The dual interface has the name of the control with a prefixed underscore.

The dispatch interface contains the events of the ActiveX object and has the name of the control with two prefixed underscores. This is a confusing convention because it is sometimes difficult to tell the difference between one and two leading underscores, but the convention works in that it now is easy to differentiate which interfaces belong to which controls.

If you compare the IDL in Listing 6.21 to the IDL in Listing 6.15, you will note that they are very similar. This is the similarity we were trying to achieve so that Visual Basic modules can take advantage of our ActiveX control.

### Events and C++Builder

Another interesting experiment is to view the content of an ActiveForm built using Inprise’s C++Builder or Delphi. Listing 6.22 shows the default IDL generated when creating an ActiveForm with C++Builder.

**Listing 6.22** IDL of C++Builder ActiveForm

```idl
// Generated IDL file by the OLE/COM Object Viewer
//
// typelib filename: <could not determine filename>
// Forward declare all types defined in this typelib
interface IActiveFormX;
dispinterface IActiveFormXEvents;

[
    uuid(18C9B680-8CA9-11D2-9C2B-DC6F06C10000),
    version(1.0),
    helpstring("ActiveFormProj1 Library")
]
library ActiveFormProj1
{
    // TLib : OLE Automation :
    // {00020430-0000-0000-C000-000000000046}
    importlib("STDOLE2.TLB");

    [
        odl,
        uuid(18C9B681-8CA9-11D2-9C2B-DC6F06C10000),
        version(1.0),
        helpstring("Dispatch interface for ActiveForm Control"),
        dual,
        oleautomation
    ]
    interface IActiveFormX : IDispatch {
        [id(0x00000001), propget]
        HRESULT _stdcall Visible(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000001), propput]
        HRESULT _stdcall Visible([in] VARIANT_BOOL Value);
        [id(0x00000002), propget]
        HRESULT _stdcall AutoScroll(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000002), propput]
        HRESULT _stdcall AutoScroll([in] VARIANT_BOOL Value);
        [id(0x00000003), propget]
        HRESULT _stdcall AxBorderStyle(
            [out, retval] TxActiveFormBorderStyle* Value);
        [id(0x00000003), propput]
        HRESULT _stdcall AxBorderStyle(
            [in] TxActiveFormBorderStyle Value);
        [id(0xffffffff), propget]
        HRESULT _stdcall Caption([out, retval] BSTR* Value);
        [id(0xffffffff), propput]
        HRESULT _stdcall Caption([in] BSTR Value);
        [id(0xffffffeb), propget]
        HRESULT _stdcall Color([out, retval] OLE_COLOR* Value);
        [id(0xfffffe00), propput]
        HRESULT _stdcall Color([in] OLE_COLOR Value);
        [id(0xfffffe00), propget]
        HRESULT _stdcall Font([out, retval] IFontDisp** Value);
        [id(0xfffffe00), propput]
        HRESULT _stdcall Font([in] IFontDisp* Value);
        [id(0xfffffe00), propputref]
        HRESULT _stdcall Font([in] IFontDisp* Value);
        [id(0x00000004), propget]
        HRESULT _stdcall KeyPreview(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000004), propput]
        HRESULT _stdcall KeyPreview([in] VARIANT_BOOL Value);
        [id(0x00000005), propget]
        HRESULT _stdcall PixelsPerInch(
            [out, retval] long* Value);
        [id(0x00000005), propput]
        HRESULT _stdcall PixelsPerInch([in] long Value);
        [id(0x00000006), propget]
        HRESULT _stdcall PrintScale(
            [out, retval] TxPrintScale* Value);
        [id(0x00000006), propput]
        HRESULT _stdcall PrintScale([in] TxPrintScale Value);
        [id(0x00000007), propget]
        HRESULT _stdcall Scaled(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000007), propput]
        HRESULT _stdcall Scaled([in] VARIANT_BOOL Value);
        [id(0x00000008), propget]
        HRESULT _stdcall Active(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000009), propget]
        HRESULT _stdcall DropTarget(
            [out, retval] VARIANT_BOOL* Value);
        [id(0x00000009), propput]
        HRESULT _stdcall DropTarget([in] VARIANT_BOOL Value);
        [id(0x0000000a), propget]
        HRESULT _stdcall HelpFile([out, retval] BSTR* Value);
        [id(0x0000000a), propput]
        HRESULT _stdcall HelpFile([in] BSTR Value);
        [id(0x0000000b), propget]
        HRESULT _stdcall WindowState(
            [out, retval] TxWindowState* Value);
        [id(0x0000000b), propput]
        HRESULT _stdcall WindowState(
            [in] TxWindowState Value);
        [id(0xfffffffe), propput]
        HRESULT _stdcall Enabled(
atfRaised = 3
} TxActiveFormBorderStyle;

typedef [uuid(18C9B688-8CA9-11D2-9C2B-DC6F06C10000),
         version(1.0)]
enum {
    poNone = 0,
    poProportional = 1,
    poPrintToFit = 2
} TxPrintScale;

typedef [uuid(18C9B689-8CA9-11D2-9C2B-DC6F06C10000),
         version(1.0)]
enum {
    mbLeft = 0,
    mbRight = 1,
    mbMiddle = 2
} TxMouseButton;

typedef [uuid(18C9B68A-8CA9-11D2-9C2B-DC6F06C10000),
         version(1.0)]
enum {
    wsNormal = 0,
    wsMinimized = 1,
    wsMaximized = 2
} TxWindowState;
};
```

If you simply skip over the default properties and events that were generated by C++Builder, you'll note again that this IDL file is almost identical to Visual Basic's IDL in Listing 6.21 and the IDL in Listing 6.15. I prefer C++Builder's convention of naming its event dispatch interface with an Events suffix rather than Visual Basic's leading underscores.

## Summary

I recognize that most developers have a fear of COM connection points and events. But my own experience is that the fear is often squashed by simply taking the time to create on your own a couple of COM controls that implement different types of events. If you're not already comfortable with events, I suggest you take the time to create your own ATL COM project that implements events. And don't stop at creating a COM server; you must also create a client that implements the events in your COM server.
