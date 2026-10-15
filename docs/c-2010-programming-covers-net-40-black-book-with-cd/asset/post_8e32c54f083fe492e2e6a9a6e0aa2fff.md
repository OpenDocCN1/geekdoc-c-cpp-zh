</authentication>
<authorization>
    <deny users="?" />
</authorization>
<membership defaultProvider="SqlProvider" userIsOnlineTimeWindow="15">
    <providers>
        <add
            name="SqlProvider"
            type="System.Web.Security.SqlMembershipProvider"
            connectionStringName="SqlServices"
            applicationName="MyApplication"
            enablePasswordRetrieval="false"
            enablePasswordReset="true"
            requiresQuestionAndAnswer="true"
            requiresUniqueEmail="false"
            passwordFormat="Hashed"
            maxInvalidPasswordAttempts="5"
            passwordAttemptWindow="10" />
    </providers>
</membership>
</system.web>
</configuration>

## The Membership Class

The Membership class allows you to create users for an ASP.NET application and manage these users. The users created for an ASP.NET application using the Membership class can access the ASP.NET application as authenticated users. The hierarchy of the Membership class is as follows:

System.Object
System.Web.Security.Membership

Table 36.21 lists the noteworthy methods of the Membership class:

| Method | Description |
|---|---|
| CreateUser() | Creates a new user for an ASP.NET application. |
| DeleteUser() | Deletes user of a specific user name. This method returns true if it deletes the user successfully and false if the user name of the user that is to be deleted does not exist. |
| FindUsersByEmail() | Returns those e-mail addresses that matches with any part of the e-mail address passed to the method. |
| FindUsersByName() | Returns the users, the user name of which matches with any part of the user name passed to the method. |
| GeneratePassword() | Provides a password of specific length. The password returned by the GeneratePassword() method contains specified number of non-alphanumeric characters. |
| GetAllUsers() | Returns users on the basis of the page index and page size passed to the method. |
| GetNumberOfUsersOnline() | Determines how many users are connected to the Internet currently. You cannot use this method if your application is using ActiveDirectoryMembershipProvider. |
| GetUserNameByEmail() | Returns the name of the user, the e-mail address of which is passed to the method. |
| UpdateUser() | Updates information of a user. |
| ValidateUser() | Verifies the credentials of a user. This method returns true if the credentials of the user are valid, otherwise false. |

## MembershipUser Class

When an instance of the MembershipUser class is obtained, the MembershipUser class helps to perform the following task directly:

- Accessing the properties involved with the MembershipUser class
- Retrieving the user password, if membership is configured for the same
- Changing the password of a user
- Changing the password hint questions and answer, if membership is configured for the same
- Resetting the password of a user
- Unlocking the user account

## Immediate Solutions

### Determining Whether Code is Verifiably Type Safe

As you learned in the In Depth section of this chapter, there may be some code that does not pass the verification process. This may be because of the limitations of the verification algorithm or the language compiler in use. For instance, the Visual C++ compiler provided with the .NET Framework is incapable of producing verifiably type-safe code. On the other hand, the C# compiler produces verifiably type-safe code. Let’s see how an application developed with Visual C++ and C# is verified by the PEVerify tool. For this, let’s create a Console application named CSharpTestApp with C# and store it in a folder named PEVerifyApps (on the CD-ROM). To create the CSharpTestApp application, perform the following steps:

- 1. Open the Visual Studio 2010 IDE by selecting Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010.

- 2. Select File→New→Project, which displays the New Project dialog box. In the New Project dialog box, select the Visual C# option in the Project types pane and the Console Application option in the Templates pane. In addition, specify CSharpTestApp as the name of the application, PEVerifyApps folder as the location, and click the OK button. The CSharpTestApp application is created.

- 3. Open the Program.cs file in the CSharpTestApp and add the code for a custom class called SimpleClass. The code for the SimpleClass class in the CSharpTestApp application is given in Listing 36.1:

### Listing 36.1: Defining the SimpleClass Class in the CSharpTestApp Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CSharpTestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            SimpleClass simpleObject = new SimpleClass();
            simpleObject.simpleMethod();
        }
    }

    class SimpleClass
    {
        public void simpleMethod()
        {
            Console.WriteLine("A simple method");
        }
    }
}
```

- 4. Compile the application.

- 5. Create a CLR Console application named VCTestApp in VC++.

- 6. In Solution Explorer, expand Source Files and double-click the VCTestApp.cpp file to open it. In the VCTestApp.cpp file, define a class named SimpleClass, as given in Listing 36.2:

### Listing 36.2: Defining the SimpleClass Class in the VCTestApp.cpp File

```
// This is the main DLL file.
#include "stdafx.h"
using namespace System;

public class SimpleClass
{
public:
void simpleMethod()
{
    Console::WriteLine("A simple method");
}
};

int main(array<System::String ^> ^args)
{
    SimpleClass simpleObject;
    simpleObject.simpleMethod();
    return 0;
}
```

As you can see in Listing 36.1 and Listing 36.2, both the applications include the same class and same functionality. However, both these applications give different results when verified using the PEVerify tool.

- 7. Compile the VCTestApp application.

- 8. Open the Visual Studio 2010 command prompt by selecting Start→All Programs→Microsoft Visual Studio 2010→Visual Studio Tools→Visual Studio 2010 Command Prompt. Now, go to the location of the CSharpTestApp.exe (which in this case is PEVerifyApps\CSharpTestApp\CSharpTestApp\bin\Debug) in the command prompt and type the following command:
peverify csharpTestApp.exe /md /il

The output of the command is:

```
Microsoft (R) .NET Framework PE Verifier. Version 4.0.30319.1
Copyright (c) Microsoft Corporation. All rights reserved.

All classes and Methods in CSharpTestApp.exe verified.
```

As you can see in the output, metadata and the MSIL code of the CSharpTestApp application have passed the verification done by the PEVerify tool. This implies that the CSharpTestApp has verifiably type-safe code.

Let's now see what happens with the VCTestApp application test. Enter the following command in the Visual Studio 2010 command prompt, after navigating to the location of the VCTestApp application:
peverify VCTestApp.exe /md /il

The output of the preceding command is:

```
Microsoft (R) .NET Framework PE Verifier. Version 4.0.30319.1
Copyright (c) Microsoft Corporation. All rights reserved.

[MD]: Unverifiable PE Header/native stub.
Unverifiable assembly 'c:\users\umer\Desktop\Chapter 36\PEVerifyApps\VCTestApp\Debug\VCTestApp.exe' failed policy check.
2 Error(s) Verifying VCTestApp.exe
```

Note that only a small chunk of the output of the verification of the VCTestApp application is shown here. As you can see in the output, the VCTestApp has failed in the verification done by the PEVerify tool and hence does not have verifiably type-safe code. There are numerous errors in the metadata verification as well as the MSIL code verification. The errors that begin with [MD] correspond to the errors in the metadata, while those that begin with [IL] correspond to the MSIL code. Note that if you do not specify the /il switch of the peverify command, then only the metadata is verified and in case of any errors in the metadata, only those errors are reported. In addition, the MSIL code is not verified if there are errors in the metadata. For instance, if you type the following command at the Visual Studio 2010 command prompt:
peverify VCTestApp.exe /md

The output of the preceding command is:

```
Microsoft (R) .NET Framework PE Verifier. Version 4.0.30319.1
Copyright (c) Microsoft Corporation. All rights reserved.

[MD]: Unverifiable PE Header/native stub.
1 Error Verifying VCTestApp.exe
```
