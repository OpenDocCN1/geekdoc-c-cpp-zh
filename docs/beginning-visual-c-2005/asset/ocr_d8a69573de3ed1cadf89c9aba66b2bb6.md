You want to be able to save a document in a file, but writing a class object to a file represents something of a problem because it isn’t the same as a basic data item like an integer or a character string. A basic data item consists of a known number of bytes, so to write it to a file only requires that the appropriate number of bytes be written. Conversely, if you know a value of type int was written to a file, to get it back you just read the appropriate number of bytes.

Writing objects is different. Even if you write away all the data members of an object, that’s not enough to be able to get the original object back. Class objects contain function members as well as data members, and all the members, both data and functions, have access specifiers; therefore, to record objects in an external file, the information written to the file must contain complete specifications of all the class structures involved. The read process must also be clever enough to synthesize the original objects completely from the data in the file. MFC supports a mechanism called serialization to help you to implement input from and output to disk of your class objects with a minimum of time and trouble.

The basic idea behind serialization is that any class that’s serializable must take care of storing and retrieving itself. This means that for your classes to be serializable — in the case of the Sketcher application, this will include the CElement class and the shape classes you have derived from it — they must be able to write themselves to a file. This implies that for a class to be serializable, all the class types that are used to declare data members of the class must be serializable too.

# Serializing a Document

This all sounds rather tricky, but the basic capability for serializing your document was built into the application by the Application wizard right at the outset. The handlers for the File > Save, File > Save As, and File > | Open menu items all assume that you want serialization implemented for your document, and already contain the code to support it. Take a look at the parts of the definition and implementation of CSketcherDoc that relate to creating a document using serialization.

# Serialization in the Document Class Definition

The code in the definition of CSketcherDoc that enables serialization of a document object is shown shaded in the following fragment:

```
class CSketcherDoc : public CDocument
{
protected: // create from serialization only
    CSketcherDoc();
    DECLARE_DYNCREATE(CSketcherDoc)

// Rest of the class...

// Overrides
public:
    virtual BOOL OnNewDocument();
    virtual void Serialize(CArchive& ar);

// Rest of the class...
};
```