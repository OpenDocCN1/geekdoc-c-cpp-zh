![](bbox=[0.193, 0.102, 0.817, 0.334])

Figure 11-20  Class diagrams for StudentGov example

The dotted arrows in Figure 11-20 represent the *interface* link. Notice that the Unified Modeling Language (UML) notation for the interfaces includes the name of the methods in italic, indicating that implementation details must be defined.

> > UML is the industry-standard modeling language for specifying and documenting both data and processes. Class diagrams are one of the modeling diagrams used with object-oriented applications. To find out more about UML, visit *www.uml.org*, the Object Management Group's Web site responsible for the release.

The *interface* object cannot have member data, just methods. The *class* diagrams do not show the properties. No accessor or mutator methods are defined for accessing or changing the *private* data members of the classes. However, during design it is decided that properties are defined with *get* and *set* behaviors for most data members. Minimal business logic is needed for this application; thus, no pseudocode or additional design tool is constructed.

**Code the Solution**  After you complete the design, it is time to translate the design into source code. For this application, six projects are created inside one solution. It is not necessary to put the files under a single solution umbrella. This was done for ease of demonstration. All of the classes could be defined as stand-alone components. The *interface* and all classes except the *PresentationGUI* could be stored in your library with other DLL files. The *PresentationGUI* generates an EXE file; all other projects generate files ending with a .dll extension.