
- Initial Toolbar. The toolbar is a row of bitmap buttons that appears beneath the application’s menu.
- Printing and Print Preview.
- Context Sensitive Help.

![](img/5e551abe6e0cb0588043ee757a235ddb_54_0.png)

Figure 4.2 shows the option dialog of AppWizard. The output of AppWizard is several C++ source and header files, the project makefile, and the resource file. Below is a list of files for an AppWizard-generated project called TEST. The TEST project uses the Single Document Interface.

- TEST.MAK — Project file compatible with Visual Workbench and command-line tool NMAKE.
- TEST.H — Main include file for application; includes other project-specific include files and declares the CTestApp application class.
- TEST.CPP — Main application source file. Contains the application class CTestApp.
- TEST.RC — Listing of all resources the program uses. It includes icons, bitmaps, and cursors stored in the RES subdirectory. File can be edited directly with App Studio.
- RES\TEST.ICO — Icon file used as application’s icon. Icon is included by the main resource file TEST.RC.

| File | Description |
|---|---|
| RES\TEST.RC2 | Contains resources not edited by App Studio. Initially contains a VERSIONINFO resource that you can customize for your application. |
| TEST.DEF | Contains information about the application that must be provided so that it runs with Microsoft Windows. Defines parameters such as name and description of application and size of initial local heap. |
| TEST.CLW | Contains information used by ClassWizard to edit existing classes or add new classes. |
| MAINFRM.H and MAINFRM.CPP | Contain frame class CMainFrame, which is derived from CFrameWnd and controls all SDI frame and features. |
| TESTDOC.H and TESTDOC.CPP | Contain the CTestDoc document class. |
| TESTVIEW.H and TESTVIEW.CPP | Contain the CTestView view class. |
| STDAFX.H and STDAFX.CPP | Used to build a precompiled header file to make and compile substantially faster. |
| RESOURCE.H | Defines resource IDs. App Studio reads and updates this file. |

**FIGURE 4.2.**  
*AppWizard options.*

![](img/5e551abe6e0cb0588043ee757a235ddb_55_0.png)

## App Studio

App Studio is used to create and edit Windows resources. With it, you can manipulate the resources for menus, dialog boxes, bitmaps, icons, cursors, strings in a string table, and keyboard accelerators. App Studio automatically generates unique resource IDs for the resources you create. These IDs are stored in the RESOURCE.H file by default. Figure 4.3 shows App Studio editing the resource file from the TEST project listed previously.

**FIGURE 4.3.**  
*App Studio.*

![](img/5e551abe6e0cb0588043ee757a235ddb_56_0.png)

## ClassWizard

ClassWizard is perhaps the most empowering component of the Visual C++ development environment. With it, you can derive classes from several standard MFC base class objects and to add member functions and variables to those classes. ClassWizard is used to map Windows messages, as well as user-defined messages, to specific member functions. With just a few mouse clicks, you can associate a specific message to a particular function name. ClassWizard creates the function prototype for that function in the header file for the class and also creates a stub function for you to add code to in the C++ file.

A common use of ClassWizard is to associate a class derived from CDialog with a dialog resource created with App Studio. First you design a dialog resource with App Studio and then launch ClassWizard. If ClassWizard is launched directly from App Studio and the dialog resource being edited doesn’t yet have a class associated with it, ClassWizard will automatically prompt you for a class name for the new dialog box class. Once the basic class is created, you can link member functions to the buttons and controls of the dialog box. You can also associate variables to the controls of the dialog box. For example, if the dialog box contains an edit control used to enter a numeric value, you can link an integer variable to that control. The integer variable becomes a member variable to the dialog’s class object. When your application needs the value entered into that edit control, it simply references the integer member variable.

**FIGURE 4.4.**  
*ClassWizard.*

![](img/5e551abe6e0cb0588043ee757a235ddb_57_0.png)

## Class Browser

The Class Browser is integrated into Visual Workbench. You can use it to view class hierarchical relationships. You can select a class and view all classes derived from it or view the class from which it was derived. Figure 4.5 shows the base class graph of the CTestApp object from the TEST application. The browser shows us that CTestApp is derived from CWinApp. Clicking CTestApp reveals specific information for that object in the other part of the class browser view. The upper-right portion shows the member functions particular to CTestApp. Double-clicking one of these names puts you into the Visual Workbench editor at the appropriate spot in the source file for CTestApp. The lower-right portion shows the source files where the CTestApp object is implemented.

**FIGURE 4.5.**  
*Class Browser.*

![](img/5e551abe6e0cb0588043ee757a235ddb_57_1.png)

## Message Mapping in an MFC Program

You will remember from the discussion in Chapter 3 that Windows is an event-driven operating system that relies on messages being delivered to the appropriate destination window in order for program execution to take place. Visual C++ makes the coding of message-based code almost trivial. With ClassWizard, you can define an object derived from a list of standard MFC objects. These base class objects are windows that expect to receive messages. ClassWizard allows for an easy mapping between messages and functions that perform the desired operations in response to those messages. After creating your derived class from the applicable base class, ClassWizard will create the member functions that you need to run in response to a message stimulus. A member function is created in the class declaration and a stub code for the member function is inserted into the implementation file for the class. The base classes from which your classes can be derived already have many member functions ready to be overridden by your special purpose code. One of these member functions reacts in response to the WM_CHAR message, which tells the window that the user has pressed a key on the keyboard. Figure 4.4 shows ClassWizard with the WM_CHAR message mapped to OnChar. The code created by ClassWizard in the class declaration for the TEST application follows:

```cpp
class CTestView : public CView
{

...

//{{AFX_MSG(CTestView)
    afx_msg void OnChar(UINT nChar, UINT nRepCnt, UINT nFlags);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```

Notice that the code ClassWizard adds is placed between the commented lines //{{AFX_MSG(CTestView) and //}}AFX_MSG. The appropriate code in the implementation file follows:

```cpp
...
```

```cpp
BEGIN_MESSAGE_MAP(CTestView, CView)
    //{{AFX_MSG_MAP(CTestView)
    ON_WM_CHAR()
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()

...
```

```cpp
void CTestView::OnChar(UINT nChar, UINT nRepCnt, UINT nFlags)
{
    // TODO: Add your message handler code here and/or call default
    CView::OnChar(nChar, nRepCnt, nFlags);
}
…
```

When a WM_CHAR message comes in that is destined for the CTestView window, the message map is examined to see how the message should be routed. Because ON_WM_CHAR is in the message map, MFC knows that the application has a message handler in place. The WM_CHAR message is one for which there is a default handler already in place in CTestView’s base class of CView. MFC knows that WM_CHAR maps to the OnChar member function. You will see in a later chapter how to add user-defined message handlers that are unique to your application. Because MFC doesn’t know of these message handlers, you have to specify in the message map the name of the member function that handles that message.

## Support Files for Building WinSock Applications

To compile an application that uses the WinSock API, you need the WinSock header file WINSOCK.H, which contains all the function prototypes and structure definitions. Linking the application requires either WINSOCK.LIB or WSOCK32.LIB depending on whether you’re targeting the 16-bit or 32-bit Windows platform. WINSOCK.H and WSOCK32.LIB are included with Visual C++ 1.1 for Windows NT. WINSOCK.H and WINSOCK.LIB are available from your TCP/IP stack provider.

To ensure source code compatibility between the 16-bit and 32-bit programs, the standard 16-bit Windows include file VER.H must be named WINVER.H, as it is named in the 32-bit environment. If you’re using a 16-bit compiler, I suggest going into the compiler’s include directory and copying VER.H to WINVER.H.

A detailed discussion of how to build WinSock applications is included in Chapter 8, “Sample Applications.”

## Summary

The Visual C++ integrated development environment has greatly simplified development of Windows programs. The well-integrated tools make it easy to create applications that use the MFC library. The WinSock class library developed later in this book will make extensive use of MFC’s functionality. The development of these classes will show the power and flexibility of Visual C++.
