Within the SAPUI5 content itself, all the resource references are pretty well self-contained. The only notable items here worth mentioning from an SAP HANA perspective are the location of the SAPUI5 library files and the target OData service.

In Listing 5.4, you can see that the SAPUI5 core library file is being loaded from a relative URL /sap/ui5/1/resources/sap-ui-core.js. Here, the 1 represents the latest-and-greatest version of the SAPUI5 library that's deployed on the SAP HANA XS engine. As long as our applications point here, we needn't worry about amending resource links in the long run.

```
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

# Listing 5.4 Accessing the SAPUI5 Library from an SAP HANA XS Application

To access the OData service, simply plug in the relative path to the XS OData file created in Section 5.4.2 (e.g., /model/BookService.xsodata). As you might expect, this implies that we can access the OData service directly in a browser by prepending the physical path of our SAP HANA XS application to the relative URL of the XS OData file. We'll explain how to run these kinds of tests in Section 5.6.

For brevity's sake, we don't really have more to say about the nitty-gritty details of the SAPUI5 content here. If you're interested in learning more about SAPUI5 technology, we'd recommend that you take a look at Getting Started with SAPUI5 (Antolovic, SAP PRESS, 2014). You can also find a wealth of information in the official SAPUI5 documentation available online at https://sapui5.netweaver.ondemand.com/sdk.