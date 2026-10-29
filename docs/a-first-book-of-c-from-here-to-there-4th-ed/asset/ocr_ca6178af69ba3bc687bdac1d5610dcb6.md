streambuf class and general routines for transferring text data. From these two base classes, several other classes are derived and included in the iostream class library.

Figure 9.4 is an inheritance diagram for the ios family of classes as it relates to the ifstream, ofstream, and fstream classes. Figure 9.5 is an inheritance diagram for the streambuf family of classes. In these diagrams, the arrows point from a derived class to a base class, so they’re actually easier to read from top to bottom. For example, Figure 9.4 indicates that all the stream objects shown are derived from the ios class, and the ifstream class is derived from both the fstream and istream classes. In all cases, a derived class has full access to all methods of its base class.

![](bbox=[0.22, 0.36, 0.8, 0.72])

Figure 9.4 The base class ios and its derived classes

![](bbox=[0.28, 0.77, 0.72, 0.93])

Figure 9.5 The base class streambuf and its derived classes

Table 9.6 lists the correspondence between the classes shown in Figures 9.4 and 9.5, including the header files defining these classes.