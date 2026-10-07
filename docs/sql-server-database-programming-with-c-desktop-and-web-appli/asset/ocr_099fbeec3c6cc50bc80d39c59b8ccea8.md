# SQL Server Database Programming with C#

![](bbox=[0.187, 0.087, 0.812, 0.416])

9.120 Running result of updating a student record.

Now we have completed all developments for the data updating and deleting actions in our client side. Before one can run this client project to access our Web service to perform data actions for any student record, make sure that all student image files should have been stored in a local folder in your machine to enable you to select one from an updated student's image as the project runs. All student image files can be found from a folder Images@Students folder located on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1). The reason for this is because we will use a virtual folder or path to save those student images for our Web project to enable them to be found during the project runs.

First run our Web service WebServiceUpdate Project, and then run our client project WebClientSQLUpdate Project by clicking the ILS Express button The running status of our client project is shown in Figure 9.120.

As we before, we want to update a student record, Tom Erica, to a new different or with an updated student image. Then, on the opened student page, enter the data items as an updated student record in the following text:

| Student ID | T77896 |
| Name | Toney Black |
| GPA | 3.20 |
| Credits | 52 |
| Major | Information System Engineering |
| Year | Sophomore |
| Email | tblack@college.edu |

Now to the FileUploadImage control and click on the Browse button to browse to the virtual folder or path where all student image files are located