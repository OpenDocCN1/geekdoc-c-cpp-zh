value of that column must be converted to a string using the toString() method. If a typed DataSet is used, you can directly use the column name (no string to convert) to access that column without needing to use the toString() method. Each piece of information returned is assigned to the associated textbox, and will be displayed there. For the faculty image, a forced conversion is performed and a system method FromStream() is used to convert and display it in the Faculty Image box.

At this point we have finished all coding for this Windows-based Web service client project. We now start to run this client project to interface with our Web service, and furthermore to access and use the Web methods to perform our query.

Wait a moment! There is one issue you need to note before you can run this project, which is you must run our Web service WebWebServiceSelect first to allow our service available to all clients. Otherwise, you may encounter some exceptions (as the Web service or remote computer cannot be found) during your client project runs.

Open Visual Studio.NET and our Web service project WebWebServiceSelect, and click on the IIS Express to run it. One point is that our service project must be kept in the running status (even if has been minimized) in order to allow our client project to access and interface with it. An exception will be encountered if you stop our Web service when you try to access it from our client project.

Make sure that our Web service has been run once and it is in the running status, which can be identified by a small IIS icon on the task bar of your screen. You may need to click on the icon by right clicking on it and select Show All Applications item. The opened running status of this Web service project is shown in Figure 9.37.

Then start our client project by clicking the Start button from the project WinClientSelect Project. The running status is shown in Figure 9.38.

Select any query method and a faculty name, such as Jenny King, from the Faculty Name combo-box, and click the Select button to call the associated Web service method to retrieve the desired faculty record. The returned faculty record is displayed in the associated textboxes with the faculty photo, which is shown in 9.38.

You can select any other Web service method, either the Stored Procedure or the DataSet method, and other faculty members to perform this data query. The running result confirmed that

![](bbox=[0.273, 0.653, 0.721, 0.901])

FIGURE 9.37 The running status of our web service WebWebServiceSelect project.