The same mechanism is carried out by the run-time executes operations on xlSheet.

Visual Basic 2010 improves this mechanism by integrating the binding with the Dynamic Language Run-time (DLR). If a late-bound call is made to an object that implements the IDynamicMetaObjectProvider interface of the System. Dynamic namespace, Visual Basic binds to the object by using dynamic. If a late-bound call is made to an object that does not implement the IDynamicMetaObjectProvider interface, or if the call to the IDynamicMetaObjectProvider interface fails, Visual Basic binds to the object by using the late-binding capabilities of the Visual run-time—just as it did before DLR integration.

From a Basic syntax point of view, the DLR integration is transparent. You cannot see any difference between a late-bound COM object or a dynamic object (an implementing IDynamicMetaObjectProvider). What you can observe is now Visual Basic binds to objects from dynamic languages such as IronPython and IronRuby. The world within which you operate from Visual Basic is definitely larger than it was before.

# THE DYNAMIC LANGUAGE RUN-TIME

> An important component in the underlying implementation of dynamic lookup is the Dynamic Language Run-time (DLR), which is a part of .NET Framework 4.0. DLR is a run-time environment that allows a set of services for dynamic languages to the Common Language Run-time (CLR), and makes it easier to develop dynamic languages to run on the .NET Framework, as well as to develop dynamic features to statically typed languages. DLR is built on top of CLR, and uses run-time binders to access the physical object model addressed by dynamic expressions. Chapter 10 provides more details about DLR.

# Accessing an IronPython Library

To learn how it is to use an IronPython library because of the DLR integration in Visual Basic, let's create a small console application that invokes an IronPython function to solve a quadratic equation. The function in IronPython will be so simple that you will be able to understand it without any Python background.

To use IronPython, you must download and install the run-time from the Downloads tab of the IronPython project's home page at http://ironpython.codplex.com.

Create new Visual Basic console application project and name it IronPythonRunner. Double-click on your project in Solution Explorer to display the project properties, and go to the References tab to add the IronPython reference assemblies. Click Add to display the Add References dialog. Use the Browse tab to navigate to the IronPython run-time's installation folder, and add the selected assemblies shown in Figure 22-1 to the project.