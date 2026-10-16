To monitor services using the Server Explorer within Visual Studio, select Servers from the tree view, and then select your computer, then the Services element. You can see the status of all services as shown in Figure 39.13. By selecting a service, you can see the properties of the service.

![](bbox=[0.0, 0.15, 1.0, 0.8])

Figure 39.13

# Writing a Custom Service Controller

In this section, you create a small WPF application that uses the ServiceController class to monitor and control Windows Services. Create a WPF application with a user interface as shown in Figure 39.14. The main window of this application has a list box to display all services; four text boxes to show the display name, status, type, and name of the service; and six buttons. Four buttons are used to send control events, one button is used for a refresh of the list, and one button is used to exit the application.