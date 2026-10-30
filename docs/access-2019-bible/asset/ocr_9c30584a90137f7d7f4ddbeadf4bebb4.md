# FIGURE 31.7

A splash screen not only increases perceived speed of your application, but it also gives your application a professional appearance.

![](bbox=[0.185, 0.189, 0.615, 0.551])

In addition, you might want to include the licensee information and/or a picture on the splash screen. If you use a picture on your splash screen, make it relevant to your application’s function. For example, some coins and an image of a check could be used for a check-writing application. If you want, you can also use clip art for your splash screen—just be sure that the picture is clear and concise and doesn’t interfere with the text information presented on your splash screen.

To implement the splash screen, have your application load the splash form before it does anything else. (Consider making your splash screen the Display Form in the Application Options, described earlier in this chapter.) When your application finishes all its initialization procedures, close the form. Make the splash form a light form and convert any bitmaps that you place on your splash screen to pictures in order to decrease the splash form’s load time.

# An application switchboard

An application switchboard is a road map for users to find their way through the functions and forms that are available in the application. Use the switchboard itself as a navigation form, using buttons to display other forms, as shown in the switchboard