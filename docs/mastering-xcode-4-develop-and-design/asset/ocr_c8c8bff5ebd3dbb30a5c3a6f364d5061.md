![](bbox=[0.067, 0.17, 0.863, 0.191])

**FIGURE 14.8** More (to the row) than meets the eye

![](bbox=[0.067, 0.26, 0.864, 0.441])

**FIGURE 14.9** Choosing keys

**FIGURE 14.10** Some example document types

The Custom Mac OS X Application Target Properties section lists all the basic parts of the property list that define your unique application (including version number, the principal class used to load the application, the main nib or xib file to use, and so on). Selecting an individual row reveals more aspects of the editor (Figure 14.8). Each row’s type (the key used to specify its corresponding value) can be edited by clicking the arrows to reveal a list of other available keys (Figure 14.9). Double-clicking a key or value lets you edit each directly. See the “Bundle Structures” section of the Bundle Programming Guide in Apple’s documentation for more information about the keys used and their meaning.

The Document Types section holds any document types defined for your application. Since TestApp is not a document-based application, this section is empty by default. That’s not to say a non-document-based application can’t be given document types that it can recognize and provide viewing or editing capabilities for, however. Figure 14.10 shows an example of what some custom document types might look like.

The Exported UTIs and Imported UTIs sections (also empty) let you define any UTIs (Uniform Type Identifiers) your application imports or exports. Defining UTIs here is a way of letting your application “claim” (and provide icons or system services for) a particular data type as well as define new data types and lineage that your application provides. See the Uniform Type Identifiers guide in Apple’s documentation for more information.