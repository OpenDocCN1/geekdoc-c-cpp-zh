You already saw an example of a standalone application in the previous section. These applications use the Window class to create windows and dialogs that are accessed through menus, toolbars, and other UI elements. The primary purpose of a window is to host and display content, such as media, XAML pages, web pages, and documents.

Browser-hosted applications, also known as XAML browser applications (XBAPs), use pages (from the Page class) and page functions (from the PageFunction<T> class). With XBAPs, you can navigate between pages using hyperlinks. Because XBAPs are hosted in a browser (Internet Explorer 6 or later), they use a partial-trust security sandbox to enforce restrictions similar to those imposed on HTML-based applications. XBAPs can run under a full-trust sandbox, but users are prompted with a security warning dialog, enabling them to decide if they want to run the application.

# # Understanding WPF Layouts

Creating a user interface requires you to arrange controls by location and size, forming a layout that must adapt to changes in window size and display settings. WPF provides a robust layout and rendering system that handles these complexities for you. The layout system is based on relative positioning rather than fixed positioning and manages the interactions between controls to determine the layout. WPF provides several layout controls for you, and you can extend the layout system with your own customized layout controls. The default layout controls follow:

+   ▶ **Canvas**—You can think of a Canvas layout as an artist's canvas. All child controls of a Canvas must provide their own layout. Canvas should be used with caution because it provides no inherent layout characteristics and uses exact positioning. The layout system provided by a Canvas is similar to that of Windows Forms or other layout systems that use exact x and y coordinates to position controls.

▶ **DockPanel**—The child controls are aligned to the edges of the panel. By default, the last control of a DockPanel fills the remaining space.

▶ **Grid**—The child controls are positioned by rows and columns, much like a table.

▶ **StackPanel**—The child controls are stacked either vertically or horizontally.

▶ **WrapPanel**—The child controls are arranged in a left-to-right order and wrapped to the next line when there are more controls than will display in the space provided. A WrapPanel also supports a top-to-bottom order, in which