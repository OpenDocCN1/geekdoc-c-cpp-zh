# Chapter 2

# The OpenGL Graphics Pipeline

+   2.1  *The OpenGL Pipeline* ................................................8
+   2.2  *Detecting OpenGL and GLSL Errors* ....................................23
+   2.3  *Reading GLSL Source Code from Files* ................................26
+   2.4  *Building Objects from Vertices* .....................................27
+   2.5  *Animating a Scene* ..................................................28
+   2.6  *Organizing the C++ Code Files* ......................................31
+        *Supplemental Notes* .................................................32

![](bbox=[0.44, 0.432, 0.581, 0.454])

OpenGL (Open Graphics Library) is a multi-platform 2D and 3D graphics API that incorporates both hardware and software. Using OpenGL requires a graphics card (GPU) that supports a sufficiently up-to-date version of OpenGL (as described in Chapter 1).

On the hardware side, OpenGL provides a multi-stage *graphics pipeline* that is partially programmable using a language called **GLSL** (OpenGL Shading Language).

On the software side, OpenGL’s API is written in C, and thus the calls are directly compatible with C and C++. Stable language *bindings* (or “wrappers”) are available for more than a dozen other popular languages (Java, Perl, Python, Visual Basic, Delphi, Haskell, Lisp, Ruby, etc.) with virtually equivalent performance. This textbook uses C++, probably the most popular language choice. When using C++, the programmer writes code that runs on the CPU (compiled, of course) and includes OpenGL calls. We will refer to a C++ program that contains OpenGL calls as a *C++/OpenGL application*. One important task of a C++/OpenGL application is to install the programmer’s GLSL code onto the GPU.

An overview of a C++-based graphics application is shown in Figure 2.1, with the software components highlighted in pink.