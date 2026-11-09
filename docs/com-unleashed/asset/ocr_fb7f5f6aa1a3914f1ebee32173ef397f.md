![](bbox=[0.071, 0.106, 0.812, 0.439])

# Visual InterDev

Visual InterDev 6.0 is Microsoft's newest development tool for Internet applications, particularly if ASP scripting is involved. Figure 1.4 illustrates its place in the DNA. Many good books have been written on Visual InterDev, and I won't attempt to introduce its many features or functions here. However, if you are already working with VI or plan to, here are some guidelines you can follow to make programming with COM and COM+ more productive.

# Avoid Data-Bound Controls

The use of data-bound DTCs (Design Time Controls) was mentioned earlier in the chapter to highlight their prototyping qualities. However, it's important to note that in general, any introduction of coupling across logical programming boundaries, such as between the GUI and database, is a bad idea. (Design of multitiered architectures is covered in Chapter 2.) VI provides a set of SQL-ready DTC controls to quickly develop Web applications that access databases directly. There are some legitimate cases in which this sort of rapid development is required.

If you are creating a small intranet Web, for example, and must do it as quickly and reliably as possible, data-bound controls are a good option. If you choose to use the controls as opposed to delegating the logic to external components, you should be aware of risking a rewrite in the future if your application ever must be ported to another programming environment that doesn't support VI6 controls (like Win32).