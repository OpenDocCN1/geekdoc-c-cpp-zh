begin with # and continue to the end of the line (see Section 4.1, ‘Introduction to ACD file development’).

An ACD file includes an application definition describing the application itself, and one or more data definitions describing the parameters. Definitions have attributes which describe the application or parameter in detail. Data definitions are organised into sections in the file such as “Input”,“Output” and so on. The ACD file is parsed when generating the application documentation. The components used include:

+   - The application name (from the application definition) and short description (from the `documentation:` attribute of the application definition)
+   - Example data files (from the “Input” section)
+   - Command line synopsis
+   - Table of application options (from the data definitions)
+   - List of links to related applications (from the `groups:` attribute of the application definition).

Therefore you should ensure that the application ACD file is valid and properly formatted by using utilities provided for this purpose.

# 8.2.1.1 Application quality assurance test

The command line sessions from the application QA tests are included in the application documentation. You should therefore write these tests and run them (see Section 7.2, ‘Application quality assurance’) before documenting the application to make sure that the example files will be correctly generated.

If you did not write the QA test before documenting the application, rerun `autodoc.pl` and it will create the remaining three include files (usage examples and input and output files), with complete HTML documentation created in `embassy/myemboss/emboss_doc/html/myprogram.html`

# 8.2.2 Sections of application documentation

Sections in the application documentation are described in the table below.

# 8.2.3 Application documentation process

The process for generating the application documentation combines manually written components with parts that are generated automatically (mostly from parsing the ACD file and from the QA tests). The process is largely automated and involves running the `autodoc.pl` script which generates a part-completed ‘application template’ which you complete by hand.

The application name and index terms are written directly to the application template. However, most of the automatically generated content is kept in ‘include files’ that are generated from template XML include files.

`autodoc.pl` is included in the EMBOSS distribution under the `scripts` directory, e.g.

```
/home/auser/emboss/emboss/scripts/autodoc.pl
```