Take a look at project metadata for a moment. MVC4WPF is an open source project that I participate in, and it uses metadata in the form of contract files to generate code. (Check it out at http://mvc4wpf.codeplex.com/.)

In a classic example of an automation pattern, MVC4WPF's New File dialog box (see Figure 4-1) checks with the user to get the contract (in the form of an interface) that is being referenced for the given Model, View, or Controller being generated.

![](bbox=[0.249, 0.293, 0.516, 0.454])

**Figure 4-1:** Selecting controller interfaces.

This allows T4 to parse through the interface, grab pertinent information, and add it to the resultant file.

# ## *Setting Up the Environment*

You need to know a few details relating to the environment.

# ### *Changing the security settings*

You can relax the security requirements for T4. If you write T4 documents and don't sign them (which is often the case), you will receive a dialog box warning you that you might be generating some dangerous code. You can see that message in Figure 4-4. You can change the option to show this message in the Security Options dialog box, shown in Figure 4-2.

As T4 files are essentially macros, this warning makes sense. It is possible for someone to write malicious code and execute it on your development workstation. I advise that you turn off the security during development of the template and back on when you are back to your daily scheduled programming.