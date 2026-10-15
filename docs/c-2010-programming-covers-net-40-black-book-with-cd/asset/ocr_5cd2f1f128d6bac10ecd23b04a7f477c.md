```
```csharp
public class TypeSharingWebService2 : System.Web.Services.WebService {
    public TypeSharingWebService2() {
        //Uncomment the following line if using designed components
        //InitializeComponent();
    }

    public class EmpDetails
    {
        public string EmpFirstName;
        public string EmpMiddleName;
        public string EmpLastName;
        public string EmpID;
        public string EmpDesignation;
    }

    [WebMethod]
    public EmpDetails updateEmpDetail(EmpDetails name, string FID, string FDesignation)
    {
        //EmpDetails name = new EmpDetails();
        name.EmpID = FID;
        name.EmpDesignation = FDesignation;
        return name;
    }

    //[WebMethod]
    //public string HelloWorld() {
    //    return "Hello World";
    //}
}
```
```

3. In the DataSharingWebService Web application, add the Web references of both the Web services one by one in the Web application. After adding the Web references, Solution Explorer displays both the Web services, as shown in Figure 18.23.

![](bbox=[0.335, 0.505, 0.606, 0.761])

4. Now, add four Label controls and two Button controls in the DataSharingWebService Web application by dragging the controls from the Toolbox to the Default.aspx page or by adding the code in the Default.aspx page of the Web application, as shown in Listing 18.18:

# Listing 18.18: Code for the Default.aspx Page

```
```aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
```
```