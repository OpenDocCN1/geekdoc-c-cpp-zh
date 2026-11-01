# Simple Web Application

Creating an installation package for a web application is not that different from creating a client install package. The download examples include a WebClient that also utilizes the AppSupport.dll assembly. You can create the deployment project the same way that the client deployment projects are created, either standalone or in the same solution. In this example, the deployment project is built in the same solution.

Start the WebClient solution and add a new deployment and setup project. This time, be sure to choose Web Setup Project in the Templates window. If you look at the properties view for the project, you will see that all the same properties exist for web applications that existed for client applications. The only addition is Restart IIS Service. This is a Boolean value that will restart IIS during the install. If you're using ASP.NET components and not replacing any ATL or ISAPI DLLs, you shouldn't have to do this.

If you look at the File System editor, you will notice that there is only one folder. The Web Application folder will be your virtual directory. By default, the name of the directory is the name of the deployment project, and it is located below the web root directory. The following table explains the properties that can be set from the installer. The properties discussed in the previous section are not included.

| PROPERTY | DESCRIPTION |
|---|---|
| AllowDirectoryBrowsing | A Boolean value that, if true, allows an HTML listing of the files and subfolders of the virtual directory. Maps to the Directory browsing property of IIS. |
| AllowReadAccess | A Boolean value that, if true, allows users to read or download files. Maps to the Read property of IIS. |
| AllowScriptSourceAccess | A Boolean value that, if true, allows users to access source code, including scripts. Maps to Script source access in IIS. |
| AllowWriteAccess | A Boolean value that, if true, allows users to change content in write-enabled files. Maps to the Write property of IIS. |
| ApplicationProtection | Determines the protection level of applications that are run on the server. The valid values are: Low — Applications run in the same process as web services. Medium — Applications run in same process but not the same as web services. High — Application runs in its own process. Maps to the Application Protection property in IIS. Has no effect if the IsApplication property is false. |
| AppMappings | A list of application names and document or data files that are associated with the applications. Maps to the Application Mappings property of IIS. |
| Condition | A Windows Installer condition that must be met for the item to be installed. |
| DefaultDocument | The default or startup document when the user first browses to the site. |
| ExecutePermissions | The level of permissions that a user has to execute applications. The valid values are: None — Only static content can be accessed. ScriptsOnly — Only scripts can be accessed. Includes ASP. ScriptsAndExecutables — Any files can be accessed. Maps to Execute Permissions in IIS. |
| Index | Boolean value that, if true, would allow indexing of the content for Microsoft Indexing Service. Maps to the Index this resource property of IIS. |