# ASP.NET AJAX-Enabled Web Site Configuration

Most of the configuration required for ASP.NET AJAX is supplied for you by default, and you only really need to add to web.config if you want to change these defaults. For example, you can add a <system.web.extensions> section to provide additional configuration. Most of the configuration that you can add with this section concerns Web services and is contained in an element called <webServices>, which in turn is placed in a <scripting> element. First, you can add a section to enable access to the ASP.NET authentication service through a Web service (you can choose to enforce SSL here if you wish):

```
<system.web.extensions>
    <scripting>
        <webServices>
            <authenticationService enabled="true" requiresSSL="true" />
        </webServices>
    </scripting>
</system.web.extensions>
```

Next, you can enable and configure access to ASP.NET personalization functionality through the profile Web service:

```
<profileService enabled="true"
    readAccessProperties="propertyname1,propertyname2"
    writeAccessProperties="propertyname1,propertyname2" />
```

The last Web service-related setting is for enabling and configuring access to ASP.NET role functionality through the role Web service:

```
<roleService enabled="true"/>
</webServices>
```

Finally, the <system.web.extensions> section can contain an element that enables you to configure compression and caching for asynchronous communications:

```
<scriptResourceHandler enableCompression="true" enableCaching="true" />
</scripting>
</system.web.extensions>
```

# Additional Configuration for the AJAX Control Toolkit

To use the controls in the AJAX Control Toolkit, you can add the following configuration to web.config:

```
<controls>
    ...
    <add namespace="AjaxControlToolkit" assembly="AjaxControlToolkit"
    tagPrefix="ajaxToolkit" />
</controls>
```

This maps the toolkit controls to the ajaxToolkit tag prefix. These controls are contained in the AjaxControlToolkit.dll assembly, which should be in the /bin directory for the web application.

Alternatively, you could register the controls individually on web pages using the <%@ Register %> directive:

```
<%@ Register Assembly="AjaxControlToolkit" Namespace="AjaxControlToolkit"
    TagPrefix="ajaxToolkit" %>
```

# Adding ASP.NET AJAX Functionality

The first step in adding Ajax functionality to a web site is to add a ScriptManager control to your web pages. Next, you add server controls such as UpdatePanel controls to enable partial-page rendering and dynamic controls such as those supplied in the AJAX Control Toolkit to add usability and glitz to your application. You may also add client-side code, and you can use the AJAX Library for further assistance in customizing and enhancing the functionality of your application.

In this section, you learn about the functionality you can add using server controls. Later in this chapter you look at client-side techniques.