```
SOURCES = addressbook.h \
editdialog.h \
abitem.cpp \
addressbook.cpp \
editdialog.cpp \
main.cpp
FORMS = editdialog.ui
RC_FILE = qaxserver.rc
```

The qaxserver.rc file referred to in the .pro file is a standard file that can be copied from Qt's src\activeqt\control directory.

Look in the example's vb directory for a Visual Basic project that uses the Address Book server.

This completes our overview of the ActiveQt framework. The Qt distribution includes additional examples, and the documentation contains information about how to build the QAxContainer and QAServer modules and how to solve common interoperability issues.