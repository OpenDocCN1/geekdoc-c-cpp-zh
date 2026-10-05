# Exercise 6.4: IDE for layered programs

This exercise is a major design project: the invention of and development of an IDE (Integrated Development Environment) for layered systems.

The idea of layered programs, using layered data and layered procedures, is a very nice idea. The goal is to be able to annotate programs with useful and executable metadata—such as type declarations, assertions, units, and support—without cluttering the text of the base program. However, the text of the program must be linked with the text of the annotations, so that any part of the program is edited, the related layers are also edited. For example, suppose it is necessary to edit the base procedure of some layered procedure. The layers may be information like type declarations or how it handles units and support sets. It would be nice for the editor to show us these layers and how they are connected to the text of the base program, when necessary. Perhaps edits to the text of the base program entail edits to the annotation layers. Sometimes this can be done automatically, but often the programmer must edit the layers.

+   a. Imagine what you would like to see in an IDE to support the development of layered systems. What would you like to see on a screen? How would you keep the parts that are edited synchronized?

+   b. Emacs is a powerful infrastructure for building such an IDE. It supports multiple windows and per-window editing modes. It has syntactic support for many computer languages, including Scheme. There are Emacs subsystems, including org-mode, that have the flavor of a layered structure for documents. Can this be extended to help with layered programming? Sketch out a way to build your IDE using Emacs.

+   c. Build a small but extensible prototype on the Emacs base, and try it out. What problems do you encounter? Did Emacs really provide a good place to start? If not, why not? Report on your experiment.