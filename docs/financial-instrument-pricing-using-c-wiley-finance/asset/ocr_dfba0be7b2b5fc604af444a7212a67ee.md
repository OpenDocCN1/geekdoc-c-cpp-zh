```
// Abstract interfaces
interface IDraw
{ // Present information

    virtual void __stdcall display() = 0;
    virtual void __stdcall print() = 0;
};

interface ISave
{ // Save to permanent storage

    virtual void __stdcall saveXML() = 0;
    virtual void __stdcall saveDB() = 0;
};

// Interface implementation
class CA : public IDraw, public ISave
{
public:

    // Implement interface IDraw.
    virtual void __stdcall display()
    {std::cout << "CA::display" << std::endl;}
    virtual void __stdcall print()
    {std::cout << "CA::print" << std::endl;}

    // Implement interface ISave.
    virtual void __stdcall saveXML()
    {std::cout << "CA::saveXML" << std::endl;}
    virtual void __stdcall saveDB()
    {std::cout << "CA::saveDB" << std::endl;}
};
```

We first note that this code is still C++ and not COM code. Second, this code contains the Microsoft-specific extension to the compiler called __stdcall. This is a somewhat technical issue and it is concerned with method arguments, how they are pushed onto the stack and who (whether it is the caller or the callee) removes them from the stack. The general options are:

+   - **cdecl**: arguments are pushed onto the stack in reverse order, that is from right to left and the caller (calling function) cleans up the stack. This is the C language convention.
+   - **pascal**: arguments are pushed onto the stack from left to right and the callee cleans up the stack. This was the calling convention in the Win16 operating system.
+   - **stdcall**: this is the standard and most common calling convention. It is a variation of the pascal calling convention and in this case the callee cleans the stack but the parameters are pushed onto the stack from right to left. It is the convention used by the application programming interfaces in the Win32 operating system.