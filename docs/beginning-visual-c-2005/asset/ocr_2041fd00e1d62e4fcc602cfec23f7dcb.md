# Supporting the Dialog Controls

For the Pen dialog, you’ll store the selected pen width in a data member, m_PenWidth, of the CPenDialog class. You can either add the data member by right-clicking the CPenDialog class name and selecting from the context menu, or you can add it directly to the class definition as follows:

```
class CPenDialog : public CDialog
{
// Construction
public:
    CPenDialog(CWnd* pParent = NULL);    // standard constructor

// Dialog Data
enum { IDD = IDD_PENWIDTH_DLG };

// Data stored in the dialog
public:
    int m_PenWidth;                    // Record the pen width

// Plus the rest of the class definition....
};
```

If you do use the context menu for the class to add m_PenWidth, be sure to add a comment to the class definition. This is a good habit to get into, even when the member name looks self-explanatory.

You’ll use the m_PenWidth data member to set the radio button corresponding to the current pen width in the document as checked. You’ll also arrange that the pen width selected in the dialog is stored in this member, so that you can retrieve it when the dialog closes. At this point you could arrange to initialize m_PenWidth to 0 in the class constructor.

# Initializing the Controls

You can initialize the radio buttons by overriding the OnInitDialog() function that is defined in the base class, CDialog. This function is called in response to a WM_INITDIALOG message, which is sent during the execution of DoModal() just before the dialog box is displayed. You can add the function to the CPenDialog class by selecting OnInitDialog in the list of overrides in the Properties window for the CPenDialog class, as shown in Figure 16-10.