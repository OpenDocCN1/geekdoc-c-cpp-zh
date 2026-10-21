```
virtual void Draw(CDC* pDC, CElement* pElement=0); // Function to display a line
virtual void Move(CSize& aSize);                     // Function to move an element

// Constructor for a line object
CLine(CPoint Start, CPoint End, COLORREF aColor, int PenWidth);

virtual void Serialize(CArchive& ar);// Serialize function for CLine

protected:
    CPoint m_StartPoint;            // Start point of line
    CPoint m_EndPoint;              // End point of line

    CLine(void);                    // Default constructor - should not be used
};
```

The AFX_EXT_CLASS keyword indicates that the class is to be exported from the DLL. This has the effect of making the complete class available to any program using the DLL and automatically allows access to any of the data and functions in the public interface of the class. The collection of things in a DLL that are accessible by a program using it is referred to as the interface to the DLL. The process of making an object part of the interface to a DLL is referred to as exporting the object.

You need to add the keyword AFX_EXT_CLASS to all of the other shape classes, including the base class CElement. Why is it necessary to export CElement from the DLL? After all, programs create only objects of the classes derived from CElement, and not objects of the class CElement itself. The reason is that you have declared public members of CElement which form part of the interface to the derived shape classes, and which are almost certainly going to be required by programs using the DLL. If you don’t export the CElement class, functions such as GetBoundRect() will not be available.

The final modification needed is to add the directive:

```
#include <afxtempl.h>
```

to stdafx.h in the DLL project so that the definition of CList is available.

You have done everything necessary to add the shape classes to the DLL. All that remains is for you compile and link the project to create the DLL.

# Building a DLL

You build the DLL in exactly the same way as you build any other project — by using the Build | Build Solution menu option or selecting the corresponding toolbar button. The output produced is somewhat different, though. You can see the files that are produced in the debug subfolder of the project folder for a Debug build, or in the release subfolder for a Release build. The executable code for the DLL is contained in the file ExtDLLExample.dll. This file needs to be available to execute a program that uses the DLL. The file ExtDLLExample.lib is an import library file that contains the definitions of the items that are exported from the DLL, and it must be available to the linker when a program using the DLL is linked.

> If you find the DLL build fails because Elements.cpp contains an #include directive for Sketcher.h, just remove it. On my system the Class Wizard added this #include directive when creating the code for the CElement class, but it is not required.