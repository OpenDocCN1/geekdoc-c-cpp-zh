
getWeather();
}
...
gadgets.util.registerOnLoadHandler(init);
</script>
</head>
<body>
</body>
</html>

### Listing 9.4 Leveraging SAP HANA Cloud Portal Features in a Widget's HTML Content

The bulk of the heavy lifting for the weather widget is handled by a function called getWeather() that's triggered whenever the widget is initialized or refreshed. As you can see in Listing 9.5, the getWeather() function leverages the GadgetPrefs API to determine the user's preferred city and country and then utilizes those values to construct the service URL to a freely available REST-based weather lookup service hosted by OpenWeatherMap. Rather than call this service directly, the URL is passed to a separate callback function named callWeatherService() that's triggered via the Busy Indicator API. The results are then parsed by the parseWeatherResults() function, which copies the current temperature into the main HTML content area.

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>HCP Book :: Chapter 9 :: Weather Widget</title>
<script type="text/javascript">
function init() {
    ...
    getWeather();
}
}
function getWeather() {
    // Fetch the target city/country to load weather
    // information for from the user preferences:
    var userPrefs = new gadgets.GadgetPrefs();
    var city = userPrefs.getPreference("City");
    var country = userPrefs.getPreference("Country");
    // Use this data to construct the service URL:
    var serviceUrl =
    "http://api.openweathermap.org/data/2.5/find?q=" +
    city + ", " + country + "&units=metric";
// Trigger the service and open up a busy indicator:
gadgets.sap.busyIndicator.show(
    callWeatherService(serviceUrl), true);
}

function callWeatherService(serviceUrl) {
    // Trigger the service call:
    $.get(serviceUrl, parseWeatherResults);
}

function parseWeatherResults(data, status, xhr) {
    // Update the content area with the service call results:
    var userPrefs = new gadgets.GadgetPrefs();
    var city = userPrefs.getPreference("City");

    $("#weather").html(city + "&nbsp;" +
        data.list[0].main.temp + "&nbsp;deg;C");

    // Hide the busy indicator:
    gadgets.sap.busyIndicator.hide();
}

...
gadgets.util.registerOnLoadHandler(init);
</script>
</head>
<body>
...
</body>
</html>
```

### Listing 9.5 Implementing the Weather Lookup Function

In Section 9.4.3, you'll see how site administrators can personalize your weather widget to pull the weather for a particular location. In the meantime, it's a good idea to go ahead and seed these parameters with reasonable defaults so that users have a good idea about what sort of data to fill in. As you can see in Listing 9.6, you can accomplish this within the spec XML file using the <UserPref> element.

```
<?xml version="1.0" encoding="UTF-8"?>
<Module>
<ModulePrefs title="Weather Widget">
...
</ModulePrefs>
<UserPref name="City" display_name="City" datatype="string"
    default_value="Dallas" />
<UserPref name="Country" display_name="Country"
datatype="string" default_value="US" />
<Content type="html" href="weather.html" />
</Module>
```

### Listing 9.6 Defining Initial Values for the Weather Widget Preferences

Although we could have incorporated additional features into our widget's design, we hope that this simple demonstration gives you a general sense of what's possible with SAP HANA Cloud Portal features. The use of such features is not a hard requirement for widget development, but they're worth a look-see, especially if you find yourself creating lots of custom libraries for your widgets. Of course, having said that, we should point out that custom library development is not out-of-bounds with widget development. In some cases, it will make sense to blend custom or third-party libraries with SAP HANA Cloud Portal features and so on. The general rule of thumb here is just to utilize the standard features wherever possible.

## 9.3.3 Adapting Preexisting Web Applications

Now that you've seen how to adapt HTML5 applications (Section 9.3.1), you probably have a pretty good idea about how to adapt Java or native SAP HANA applications as OpenSocial widgets. Here, as was the case with HTML5 applications, you simply drop your widget's spec XML file in the application root folder and deploy the application as usual.

The only real trick to adapting preexisting applications is in dealing with cross-origin requests. For example, when adapting SAPUI5 applications, you may need to fetch the latest version of the SAPUI5 library from a content delivery network (CDN), or when calling a RESTful service, you might need to hit a URL endpoint hosted on a different server.

To address these issues, SAP provides an SAP HANA Cloud Portal-specific feature that provides access to an SAP HANA Cloud Portal proxy. From a development perspective, all you have to do to tap into this feature is define a reference to the sap-xhrwrapper feature, as demonstrated in Listing 9.7. Within the code itself, you don't have to modify URLs or filter them through some API function; the OpenSocial container will proxy the requests for you automatically.

```
<?xml version="1.0" encoding="UTF-8"?>
<ModulePrefs title="Weather Widget">
<Require feature="sap-xhrwrapper" />
...
</ModulePrefs>

<Content type="html" href="weather.html" />
</Module>
```

### Listing 9.7 Accessing the SAP HANA Cloud Portal Proxy Feature

## 9.3.4 Adding a Widget to the Portal's Content Catalog

Once you finish development on your widget application, you'll want to publish it to the Content Catalog so that site designers can begin plugging the widget into site definitions. In general, widget publication is a straightforward and simple process that follows these steps:

- 1. Deploy the hosting application to SAP HCP as usual. For example, to deploy the weather widget developed in Section 9.3.1 and Section 9.3.2, simply deploy the HTML5 application using the same steps demonstrated in Chapter 7.
- 2. Once the application is deployed, open the SAP HANA Cloud Portal Authoring Space. You can get to this Authoring Space via the SAP HCP Cockpit by navigating to the Services tab and clicking on the Go to SERVICE link for SAP HANA Cloud Portal (Figure 9.14).

![](img/cf7012644082c115a2181376d9b7486d_404_0.png)

Figure 9.14 Opening the SAP HANA Cloud Portal Authoring Space

- 3. Within the SAP HANA Cloud Portal Authoring Space, widgets are maintained on the CONTENT tab. From this tab, you can add a new widget by clicking on the Add WIDGET link shown in Figure 9.15.

![](img/cf7012644082c115a2181376d9b7486d_405_0.png)

Figure 9.15 Adding a Widget to the Content Catalog: Part 1

- 4. This will open the Add WIDGET dialog box shown in Figure 9.16. Here, you must specify the widget's type (OpenSocial in this case), its name, an optional description and icon used to identify the widget, and, most importantly, the URL for the widget's spec XML file.

![](img/cf7012644082c115a2181376d9b7486d_405_1.png)

Figure 9.16 Adding a Widget to the Content Catalog: Part 2

- 5. Once all of the widget attributes are in place, click on the Save button to add the widget to the catalog.

After the widget upload process completes, you'll see your new widget available in the Content Catalog alongside of all the standard widget types provided by SAP. In the next section, you'll see how to put these widgets to work when we demonstrate how to create new site definitions.

## 9.4 Case Study: Building a Custom Portal Site

Once you accumulate the various widget components you plan to incorporate into your site definition, the process of developing the site itself is remarkably straightforward. To demonstrate just how easy this is, in this section we'll walk you through creating a site that presents a portfolio that showcases some of the sample applications you've developed on SAP HCP throughout the course of this book.

## 9.4.1 Creating a Site in the Site Directory

As you might expect, the first step in the site development process is the creation of the site itself. This task can be carried out within the SAP HANA Cloud Portal Authoring Space, which was briefly introduced in Section 9.3.4. Here, you have two options for creating new site definitions.

The first and most straightforward option is to create the site from scratch on the Site Directory tab shown in Figure 9.17.

![](img/cf7012644082c115a2181376d9b7486d_406_0.png)

Figure 9.17 Creating a New Site Definition: Part 1
