

```java
rs.close();
pstmt.close();
conn.close();
// Display the results:
output += '</table></body></html>';
$.response.setBody(output);
```

### Listing 5.3 Server-Side JavaScript Example

## 5.5 Developing the Application UI

With the OData service created in Section 5.4.2 in tow, the development of the user interface with SAPUI5 was unremarkable in that we didn't have to introduce any SAP HANA-specific content. Indeed, if you browse through the book's source code bundle, you'll find that the UI we created contains SAPUI5 content as per usual.

This is illustrated in Figure 5.24, where you can see how we've defined lots of SAPUI5-related content files inside of our SAP HANA XS project in a folder called ui. The HTML bootstrap file (index.htm) is stored at the project root level.

![](img/cf7012644082c115a2181376d9b7486d_195_0.png)

### Figure 5.24 Embedding SAPUI5 Content in an SAP HANA XS Project

Within the SAPUI5 content itself, all the resource references are pretty well self-contained. The only notable items here worth mentioning from an SAP HANA perspective are the location of the SAPUI5 library files and the target OData service.

In Listing 5.4, you can see that the SAPUI5 core library file is being loaded from a relative URL /sap/ui5/1/resources/sap-ui-core.js. Here, the 1 represents the latest-and-greatest version of the SAPUI5 library that's deployed on the SAP HANA XS engine. As long as our applications point here, we needn't worry about amending resource links in the long run.

```html
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />

	<script src="/sap/ui5/1/resources/sap-ui-core.js"
		id="sap-ui-bootstrap"
		data-sap-ui-libs="sap.m"
		data-sap-ui-theme="sap_bluecrystal">
	</script>
	...
</html>
```

### Listing 5.4 Accessing the SAPUI5 Library from an SAP HANA XS Application

To access the OData service, simply plug in the relative path to the XS OData file created in Section 5.4.2 (e.g., /model/BookService.xsodata). As you might expect, this implies that we can access the OData service directly in a browser by prepending the physical path of our SAP HANA XS application to the relative URL of the XS OData file. We'll explain how to run these kinds of tests in Section 5.6.

For brevity's sake, we don't really have more to say about the nitty-gritty details of the SAPUI5 content here. If you're interested in learning more about SAPUI5 technology, we'd recommend that you take a look at Getting Started with SAPUI5 (Antolovic, SAP PRESS, 2014). You can also find a wealth of information in the official SAPUI5 documentation available online at https://sapui5.netweaver.ondemand.com/sdk.

## 5.6 Finishing Touches

With the bulk of the heavy lifting out of the way, there are just a few finishing touches needed to finish our sample application. In this section, we’ll take a look at several important descriptor files that are used to configure our application for external use.

### 5.6.1 Creating the Application Descriptor File

The first descriptor file we’ll be looking at is the main application descriptor file. This file must be present in order to deploy our SAP HANA XS application. To create the application descriptor file within your sample project, perform the following steps:

- 1. Right-click on the project root node and select the New • File menu option, as shown in Figure 5.25.

![](img/cf7012644082c115a2181376d9b7486d_197_0.png)

### Figure 5.25 Creating the Application Descriptor File: Part 1

- 2. This will open the New wizard dialog box shown in Figure 5.26. Within this dialog box, you can initiate the creation of the file by expanding the SAP HANA • Application Development folders and selecting the XS APPLICATION DESCRIPTOR FILE node. Click on Next > to continue.

- 3. On the confirmation screen shown in Figure 5.27, create the application descriptor by clicking on the Finish button. Note that you don’t have to specify the name of the file; the wizard has taken care of this for you automatically.

![](img/cf7012644082c115a2181376d9b7486d_198_0.png)

### Figure 5.26 Creating the Application Descriptor File: Part 2

![](img/cf7012644082c115a2181376d9b7486d_198_1.png)

### Figure 5.27 Creating the Application Descriptor File: Part 3

After the application descriptor creation wizard completes, you'll notice that a new file called .xsapp is created within the root folder. If you open up this file in a text editor, then you'll find that it's completely empty—and that's exactly as it should be. According to the SAP HANA help documentation, this file is intended to be empty (at least for the time being).

### 5.6.2 Defining the Application Access File

The next descriptor file that we'll be looking at is the application access file. This file can be created using the same procedure we demonstrated for the .xsapp file in Section 5.6.1; the only difference is that you'll want to select the XS APPLICATION ACCESS FILE option when kicking off the file creation wizard (see Figure 5.28).

![](img/cf7012644082c115a2181376d9b7486d_199_0.png)

### Figure 5.28 Creating the Application Access File

Much like the .xsapp application descriptor file described in Section 5.6.1, the generated application access file (which goes by the name .xsaccess) is initially empty. This time, though, there is some content that we'll want to fill in. In particular, we want to specify the following:

- > Because SAP HANA XS applications are hidden from public view by default, we want to set the `exposed` attribute to `true` so that we'll be able to access the application externally (e.g., via a web browser).
- > To enforce some measure of security, we'd like to turn on basic or form-based authentication so that users have to log in before accessing the SAP HANA XS application.
- > To make it easier to launch the application, we specify `index.htm` as the application's default content file. That way, users can navigate to the application root, and the SAP HANA XS engine will load the landing page automatically.

Listing 5.5 shows how we're specifying these attributes for our sample application. As you can see, the .xsaccess file utilizes a JSON-based syntax based on simple name-value pairs. You can find the complete syntax diagram for this file in the online help documentation.

```json
{
  "exposed" : true,
  "authentication" : {"method": "Basic"},
  "default_file" : "index.htm"
}
```

### Listing 5.5 Defining the Application Access File

### 5.6.3 Defining a Security Role for Display Access

When developing production-quality SAP HANA XS applications, we must formulate a comprehensive security model that ensures that every aspect of our application is secure. Here, we might need to define a series of roles and privileges that determine the scope of access offered to particular sets of users.

In order to support all of the various requirements that might crop up within a particular development project, the SAP HANA security model is very granular, allowing us to define many different types of privileges. However, for the purposes of our demo application, we'll be working with only one type of privilege: the application privilege. This privilege type is used to provide application-level access to end users.

To create our application privilege within our SAP HANA XS application, we create a new file called .xsprivileges. As you can see in Listing 5.6, this file also utilizes JSON to specify one or more privileges. Each privilege record consists of a name attribute and a description attribute. For the purposes of our demo application, we created a generic privilege called Basic that we'll assign to any authorized users.

```json
{ "privileges" :
  [ { "name" : "Basic",
      "description" : "Default User Privilege" } ]
}
```

### Listing 5.6 Defining a Simple Application Privilege for the Demo Application

Although the SAP HANA security model allows us to assign privileges directly to users, the preferred method of delivery is via a role assignment. Therefore, once we create our privilege file, the next step is to create a new role definition. This is achieved by performing the following steps:

- 1. Right-click on the project root folder and select the New • OTHER menu option.

- 2. In the New dialog box shown in Figure 5.29, select the SAP HANA • DATABASE DEVELOPMENT • ROLE option. Click on NEXT > to continue.

![](img/cf7012644082c115a2181376d9b7486d_201_0.png)

### Figure 5.29 Defining a Security Role: Part 1

- 3. On the confirmation screen, give your role a name and click on Finish (Figure 5.30). For our demo, we created a role called display_access. As the name suggests, this role will be used to provide basic display access to our application to end users.

