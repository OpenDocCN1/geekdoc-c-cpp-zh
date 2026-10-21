The Serialize() function in the document object calls the Serialize() function (or uses an overloaded insertion operator) for each of its data members. Where a member is a class object, the Serialize() function for that object serializes each of its data members in turn until ultimately basic data types are written to the file. Because most classes in MFC ultimately derive from CObject, they contain serialization support, so you can almost always serialize objects of MFC classes.

The data that you’ll deal with in the Serialize() member functions of your classes and the application document object are, in each case, just the data members. The structure of the classes that are involved and any other data necessary to reconstitute your original objects is automatically taken care of by the CArchive object.

Where you derive multiple levels of classes from CObject, the Serialize() function in a class must call the Serialize() member of its direct base class to ensure that the direct base class data members are serialized. Note that serialization doesn’t support multiple inheritance, so there can only be one base class for each class defined in a hierarchy.

# How to Implement Serialization for a Class

From the previous discussion, I can summarize the steps that you need to take to add serialization to a class:

+   1. Make sure that the class is derived directly or indirectly from CObject.
+   2. Add the DECLARE_SERIAL() macro to the class definition (and to the direct base class if the direct base is not CObject).
+   3. Declare the Serialize() function as a member function of your class.
+   4. Add the IMPLEMENT_SERIAL() macro to the file containing the class implementation.
+   5. Implement the Serialize() function for your class.

Now take a look at how you can implement serialization for documents in the Sketcher program.

# Applying Serialization

To implement serialization in the Sketcher application, you must implement the Serialize() function in CSketcherDoc so that it deals with all of the data members of that class. You need to add serialization to each of the classes which specify objects that may be included in a document. Before you start adding serialization to your application classes, you should make some small changes to the program to record when a user changes a sketch document. This isn’t absolutely necessary, but it is highly desirable because it enables the program to guard against the document being closed without saving changes.

# Recording Document Changes

There’s already a mechanism for noting when a document changes; it uses an inherited member of CSketcherDoc, SetModifiedFlag(). By calling this function consistently whenever the document changes, you record the fact that the document has been altered in a data member of the document class object. This causes an automatically displayed when you try to exit the application without saving the