Namespaces used:
Osp::Ui, Osp::Ui::Controls, Osp::Web::Controls

Header files to #include:
FUi.h, FUiControls.h, FWeb.h

Required libraries:
FUi, FUiControls, FWebControls

Required privilege level:
Normal

Required privilege groups:
WEB_SERVICE

The Web control can be used to add a web browser to an application to load web pages, download content and run JavaScript inside the browser. The Web control is based on Webkit (webkit.org). This recipe shows the two different ways that the Web control can be used. Each example details the steps required to create and use the Web control, and provides some sample code snippets.

Both examples in this recipe assume the steps detailed in Method 2 of the recipe ‘Add a Form to a Frame-based App’ have been followed to add a Form to the application’s Frame.

# Example 1: Loading a Web Page

This example creates a Web control to display a web page using the Osp::Web::Controls::Web class, and displays it in a form with a landscape orientation (see Figure R2.14).

![](bbox=[0.22, 0.86, 0.78, 0.94])

Figure R2.14 Web control.