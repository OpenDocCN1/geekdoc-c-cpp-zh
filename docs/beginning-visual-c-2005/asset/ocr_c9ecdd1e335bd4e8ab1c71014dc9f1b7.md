# Adding a Dialog Class

Right-click the dialog box that you just created in the Resource Editor pane and then select Add Class from the pop-up tool display the Class Wizard dialog. You’ll define a new dialog class derived from the MFC class CDialog, so select that class name from the Base Class: drop-down list box. You can enter the class name as CPenDialog in the Class name: edit box. The Class Wizard dialog should look as shown in Figure 16-6.

![](bbox=[0.26, 0.22, 0.85, 0.56])

Figure 16-6

Click the Finish button to create the new class.

The CDialog class is a window class (derived from the MFC class CWnd) that’s specifically for displaying and managing dialogs. The dialog resource that you have created automatically associates with an object of type CPenDialog because the IDD class member is initialized with the ID of the dialog resource:

```
class CPenDialog : public CDialog
{
    DECLARE_DYNAMIC(CPenDialog)

public:
    CPenDialog(CWnd* pParent = NULL);   // standard constructor
    virtual ~CPenDialog();

    // Dialog Data
    enum { IDD = IDD_PENWIDTH_DLG };
protected:
    virtual void DoDataExchange(CDataExchange* pDX);   // DDX/DDV support

    DECLARE_MESSAGE_MAP()
};
```