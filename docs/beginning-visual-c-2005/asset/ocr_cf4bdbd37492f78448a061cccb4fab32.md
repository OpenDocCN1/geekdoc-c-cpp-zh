# Chapter 12

```
```cpp
CTextEditorDoc();
DECLARE_DYNCREATE(CTextEditorDoc)

// Attributes
public:

// Operations
public:

// Overrides
public:
virtual BOOL OnNewDocument();
virtual void Serialize(CArchive& ar);

// Implementation
public:
virtual ~CTextEditorDoc();
#ifdef _DEBUG
virtual void AssertValid() const;
virtual void Dump(CDumpContext& dc) const;
#endif

protected:

// Generated message map functions
protected:
DECLARE_MESSAGE_MAP()
};```
```

As in the case of the previous classes, most of the meat comes from the base class and is therefore not apparent here. The macro DECLARE_DYNCREATE() that appears after the constructor (and was also used in the CMainFrame class) enables an object of the class to be created dynamically by synthesizing it from data read from a file. When you save an SDI document object, the frame window that contains the view is saved along with your data. This allows everything to be restored when you read it back. Reading and writing a document object to a file is supported by a process called serialization. You will see how to write our own documents to file using serialization and then reconstruct them from the file data in the examples we will develop.

The document class also includes the macro DECLARE_MESSAGE_MAP() in its definition to enable Windows messages to be handled by class member functions if necessary.

The view class in our SDI application is defined as:

```
```cpp
class CTextEditorView : public CEditView
{
protected: // create from serialization only
CTextEditorView();
DECLARE_DYNCREATE(CTextEditorView)

// Attributes
public:
```
```