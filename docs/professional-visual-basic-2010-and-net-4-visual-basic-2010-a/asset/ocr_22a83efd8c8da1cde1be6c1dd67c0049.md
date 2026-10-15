![](bbox=[0.14, 0.09, 0.8, 0.48])

# FIGURE 17-1

You’ll also note a new feature of Visual Studio 2010 has been highlighted in Figure 17-1. In the lower-left corner is a drop-down showing a series of percentages. Changing the value here changes the default size of the text in the XAML code window. Thus, at 200% the text in the text editor is shown at 200% normal size. This is one of the benefits of having a WPF-based editor; the vector graphics allow for scaling on-the-fly without needing to change a font size to change the size of the displayed text.

Chapter 5 also introduced the XAML that is generated with a new project, so the next step is to start customizing this newly created project.

# Implementing a Custom WPF Application

It is possible to do much of your WPF programming using XAML, but the next step is to examine how XAML can be integrated with code. After all, at some point you probably expect to start seeing some Visual Basic code again. Until now the ProVB_WPF_Step1 sample has been a pure XAML application, so first we will make a quick plan for what this application will do and then we will create a first-cut implementation. For demonstration purposes, we will create a simple photo-viewing application. The user should be able to select a folder containing one or more images and then view those images, moving forward and backward through the list.

For now, that will be the extent of the requirements; later, after the basic application is operational, you can expand the scope to customize the look and feel further. Begin by modifying the “empty” window. Of course, it’s not really empty. The window actually has a grid within it, so you can start with that and create three sections. After selecting the grid, hover over the left-hand border of your window. You’ll see a point appear within the border that sends a guide line horizontally across the window. Select a point about 40 pixels from the top and a second point approximately 40 pixels from the bottom, dividing your grid into three sections.