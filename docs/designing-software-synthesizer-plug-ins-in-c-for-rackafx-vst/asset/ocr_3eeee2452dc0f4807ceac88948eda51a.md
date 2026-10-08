```
class Component: public ComponentBase,
    public IComponent
{
    public:
        /** constructor */
        Component ();

    <SNIP SNIP SNIP>

};
```

// --- our COM creation method
static FUnknown* createInstance(void*) { return (IAudioProcessor*)new
Processor(); }

// --- our Globally Unique FUID
static FUID cid;
createInstance method creates and returns a pointer to the IAudioProcessor interface; since IAudioProcessor ultimately derives from FUnknown, the function returns the FUnknown pointer as we expect—the FUnknown pointer is always the return value from creation functions. Below that is the declaration for the FUID. At the top of the VSTProcessor.cpp file you can find the definition of the FUID named "cid":

```
FUID Processor::cid (0x91F037DC, 0xA35343AB, 0x852C37B1, 0x3774DC90);
```

In the VSTController.h file you can find the declaration for the Controller:

```
class Controller: public EditController, public IMidiMapping, public
ST3EditorDelegate
{
    public:
    <SNIP SNIP SNIP>
};
```

IMidiMapping is a "direct" interface as it inherits only from FUnknown, while EditController (like AudioEffect) is a set of interfaces many layers deep. When you see the "I", you know there is a bit more to do than just the createInstance() and FUID declarations. The VST3EditorDelegate is an object that deals with the certain kind of GUI we will implement. We need to override a few of its functions later. As before, we can find these two declarations: