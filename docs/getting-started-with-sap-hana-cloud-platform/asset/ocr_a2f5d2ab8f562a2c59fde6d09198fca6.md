```
datatype="string" default_value="US" />
```

```
<Content type="html" href="weather.html" />
```

```
</Module>
```

# Listing 9.6 Defining Initial Values for the Weather Widget Preferences

Although we could have incorporated additional features into our widget's design, we hope that this simple demonstration gives you a general sense of what's possible with SAP HANA Cloud Portal features. The use of such features is not a hard requirement for widget development, but they're worth a look-see, especially if you find yourself creating lots of custom libraries for your widgets. Of course, having said that, we should point out that custom library development is not out-of-bounds with widget development. In some cases, it will make sense to blend custom or third-party libraries with SAP HANA Cloud Portal features and so on. The general rule of thumb here is just to utilize the standard features wherever possible.

# 9.3.3 Adapting Preexisting Web Applications

Now that you've seen how to adapt HTML5 applications (Section 9.3.1), you probably have a pretty good idea about how to adapt Java or native SAP HANA applications as OpenSocial widgets. Here, as was the case with HTML5 applications, you simply drop your widget's spec XML file in the application root folder and deploy the application as usual.

The only real trick to adapting preexisting applications is in dealing with cross-origin requests. For example, when adapting SAPUI5 applications, you may need to fetch the latest version of the SAPUI5 library from a content delivery network (CDN), or when calling a RESTful service, you might need to hit a URL endpoint hosted on a different server.

To address these issues, SAP provides an SAP HANA Cloud Portal-specific feature that provides access to an SAP HANA Cloud Portal proxy. From a development perspective, all you have to do to tap into this feature is define a reference to the sap.xhrwrapper feature, as demonstrated in Listing 9.7. Within the code itself, you don't have to modify URLs or filter them through some API function; the OpenSocial container will proxy the requests for you automatically.

```
<?xml version="1.0" encoding="UTF-8"?>
```

```
</Module>
```