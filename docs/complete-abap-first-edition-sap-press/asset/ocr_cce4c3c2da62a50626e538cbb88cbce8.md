If you're a beginner, you may find the New Debugger overwhelming, so we'll start our discussion in this chapter with the Classic Debugger and then look at all the new features offered by the New Debugger. However, SAP is phasing out the Classic Debugger, and as of SAP NetWeaver 7.5, the Classic Debugger has been declared obsolete. It's no longer possible to set the Classic Debugger as the default debugger, and we recommend using the New Debugger, which is the default debugger. The major difference between the two debuggers is that the Classic Debugger loads in the same session as the program, whereas the New Debugger uses a two-process architecture so that it's loaded in a new session. The New Debugger also offers a customizable user interface with many new tools.

In Section 17.1, we'll begin by looking at the Classic Debugger features, which are similar to the New Debugger features. Specifically, we'll discuss how to activate and use the Classic Debugger and discuss the different types of views and additional features available.

Section 17.2 will then touch on the features offered in the New Debugger, including its UI and tools. From there, in Section 17.3, we'll discuss a new debugger tool as of SAP NetWeaver 7.5: the ABAP Managed Database Procedures (AMDP) Debugger.

In Section 17.4 and Section 17.5, we end the chapter by looking at how the debugging tools can enable to troubleshoot code and identify important concepts.

# ## 17.1 Classic Debugger

To understand the various features of the Classic Debugger, let's work with an example that sets up a problem and see how to go about troubleshooting the problem using this tool. For the example, assume a report isn't showing the expected output, and you want to debug the program to figure out where things are going wrong.

In this section, we'll begin by looking at how to activate and use the Classic Debugger.