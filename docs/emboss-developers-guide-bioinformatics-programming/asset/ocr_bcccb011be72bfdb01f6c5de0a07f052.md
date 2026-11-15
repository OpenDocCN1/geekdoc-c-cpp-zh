new applications. An application developed and tested in myemboss can be added to the main package or an EMBASSY package using essentially the same process.
To add an entirely new EMBASSY package you must create the directory structure and
required files, which includes the application ACD files, C source code files and
documentation, and edit the file configure.in and several Makefile.am files.
New functions and datatypes for AJAX and NUCLEUS must have structured comments
to be properly integrated with the rest of the libraries. Entirely new library files are integrated
by editing the Makefile.am in the AJAX or NUCLEUS directory as appropriate. You must
also add any new header files to ajax.h and / or emboss.h.
For more information see Section 3.2, ‘Integration and compilation’.

# 3.1.10 Debugging

Any contributed code should be as bug-free as possible. EMBOSS includes inbuilt features
for debugging applications. In addition, debugging functions are provided for fixing specific
modules of code. For further information see Section 3.3, ‘Debugging’.

# 3.1.11 Quality assurance testing

Various quality assurance tests are performed on the EMBOSS code and documentation to
maintain quality. All applications are run on test data to ensure they work as advertised.
Regular compilation and memory leak tests of the whole package ensure the integrity of the
code, for example that applications are not broken by recent changes to the library. The
structured documentation for objects and functions is validated. This ensures, for example,
that functions and parameters have meaningful and consistent names and functions are listed
in the correct section of the file.

Quality assurance testing is handled by the EMBOSS developers but there are
ways to help. Your own code should be tested thoroughly in real use-case scenarios. In
particular, it should be tested for memory leakage (see Section 3.3, ‘Debugging’)
before it is contributed: if you are unclear how to do this then ask on the EMBOSS mailing
lists (Section 1.4, ‘Project mailing lists’). Any library code for submission, or at least new
public datatypes and functions, should be documented with structured comments (see
Appendix D, Code documentation standards) so that validation checks can be performed. Any
new applications should, ideally, have test cases and test data (see Chapter 7, Quality
assurance).

# 3.1.12 Documentation

Software without documentation often has little value whereas good documentation can
enhance the usefulness of software immensely. All EMBOSS application and library code for
submission should be adequately documented. End-user documentation is also required for
any new applications.

The process for generating the application end-user documentation, which is split into
different sections, involves combining manually written components with parts that are
generated automatically (for example, from parsing the ACD file). The process is largely
automated. If you develop a new EMBASSY package then it will require documentation
above and beyond that for individual applications.