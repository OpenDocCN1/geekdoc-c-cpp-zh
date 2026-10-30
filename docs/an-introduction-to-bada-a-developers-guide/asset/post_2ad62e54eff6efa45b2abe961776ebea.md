
Osp::Io

# Declared In:

FIo.h

# Library:

FIo

# Privileges Required:

None.

# Summary

Selected important classes:

- Database
- Directory
- File

As shown in Figure 6.11, the Io namespace includes wrapper classes to handle files, directories, databases, and registries. The File class provides support for creating, deleting, writing to, and reading from files using raw buffers and strings. To get information about files and directories, use the FileAttributes class.

Applications only have write access to files in their home or shared directory – which is used to share data with other applications.

![](img/a257d5fd53a79a244a20e587cd2f08f6_196_0.png)

Figure 6.11 Core classes in the Osp::Io namespace.

The Database class provides support for basic database functions, creating and deleting databases, and executing SQL commands. It also includes support for transactions and rollback, which are very useful functions when using SQL databases. The SQL used by the Database class is SQLite (www.sqlite.org).

> Note: The database is for storage on the local device only, there is no support for connecting to remote databases.

The Registry class supports creating, writing to, and reading from registry files, which an application typically uses to store settings. This is different from the registry managed by App::AppRegistry, which only the application can access. An application could store a file created by Io::Registry in

![](img/a257d5fd53a79a244a20e587cd2f08f6_200_0.png)

Figure 6.13 The role of the LocationProvider class in the OSp::Locations namespace.

# Server Supported Services

Using the bada Server, together with the RemoteLocationProvider class, developers can also access information about remote devices, periodically report the last location of the local device to the server, and use the SubscribeToTraceService method and ITraceServiceListener class to record a path of travel.

Reporting device location to the bada Server is done using the StartLocationReport method, together with the ILocationReportListener class. This causes location information to be uploaded to the bada Server periodically, information that will then be available for other authenticated devices to read.

To retrieve the last known locations of remote devices, use the RequestLastKnownLocationList method, passing in a list of TargetInfo objects that identify a device from the user’s bada Server userID. You can also narrow down the results to devices with last known locations inside a given area using the RequestLastKnownLocationListInCircle and RequestLastKnownLocationListInRectangle methods.

# Landmarks

The Landmark class represents a named geographical location that has a name and contains extra information such as a description and a URL. Applications can create their own landmarks, from a user-selected location on a map, for example, or use pre-defined landmarks provided by other applications or third-party content providers.

![](img/a257d5fd53a79a244a20e587cd2f08f6_202_0.png)

# Figure 6.14 Classes for rendering a Map within a UI control.

The purpose of each layer and the related classes and methods for manipulating this information is as follows:

# Zoom

The top layer containing UI controls for zooming. The application implements IMapEventListener::OnMapZoomingStarted and OnMapZoomingEnded to be notified when the user zooms the map.

# Info Window

Word bubbles that display useful information about locations and businesses. This may include a brief description of a business and its contact details, for example. Info windows are created using the NativeMapInfoWindow class for pre-defined windows and IMapInfoWindow classes for user-defined windows.

# MyLocation

Displays the current location on the map, together with a circular bounds showing the margin of error. The application can choose whether to display this information by using the Map::SetMyLocationEnabled method.

# Overlay

An interactive layer with shapes marking out locations on the map and markers that can be moved by the user like pins on a physical map. Shapes – polygons, circles, and rectangles – can be included in a map by adding objects deriving from the MapOverlayShape class, while movable markers derive from MapOverlayMarker as shown in Figure 6.15.

Applications implement the IMapOverlayEventListener to handle the events received when the user moves the markers around.

# Map

The basic map graphic as provided by the map service provider and encapsulated by the Map class. Methods of this class provide lots of control over how the map is displayed, including its size and bounding rectangle.

![](img/a257d5fd53a79a244a20e587cd2f08f6_203_0.png)

Figure 6.15 Classes for adding overlays to a Map.

```
Osp::Locations::Services
```

# Declared In:

```
FLocations.h
```

# Privileges Required:

Using the features of Locations::Services requires the following privilege group:

| Privilege group | Privilege level | Description |
|---|---|---|
| LOCATION_SERVICE | NORMAL | Using the directory, geocoding, map or route services |

# Prerequisites:

An account with a geographic services provider.

# Summary

Selected important classes:

- `IDirectoryServiceProvider`
- `IMapServiceProvider`
- `IRouteServiceProvider`
- `ProviderManager`

This namespace provides support for geographic information services: maps, geocoding, directory, and route services. The starting point for implementing these services is the `ProviderManager` class, which retrieves information about the service providers available to the device and allows the application to choose the one that provides the appropriate services.

Support for map services is provided by a set of interface classes called to get map information and render the map. The `IMap` interface implements dynamic maps from the service provider, supporting features such as panning and zooming, the UI for which is handled by classes in the `Locations::Controls` namespace.

# Route and Directory Services

The Route Service is implemented by the `IRouteServiceProvider` and `IRouteServiceListener`, and allows the application to request a route, given a set of waypoints – which, at a minimum, must consist of a start and destination – and parameters such as mode of transport and whether the route is the fastest or shortest. The application is returned a list of `Routes`, which contains a set of coordinates representing the route and information such as length, estimated travelling time, and a set of `RouteSegments`. The application could then display this information on a map to provide services such as turn-by-turn directions. The classes that provide the Route Service are shown in Figure 6.16.

The Directory Service allows application developers to implement a user-friendly search for products and services within a specified geographic area – coffee shops within a certain city, for example. Developers put together their search request with the methods of `IDirectoryServiceProvider` and process the response asynchronously using `IDirectoryServiceListener`. The search results are returned as a list of `Landmarks`. Underpinning these services is the geocoding service, which converts an address into geographic coordinates and vice versa.

Note: To make use of these services, you’ll need an account with a geographic information services provider such as deCarta (www.de carta.com), which is the map provider currently supported by bada. However, you can provide access to maps within an application by using the Web::Control class and web sites such as www.googlemaps.com.

![](img/a257d5fd53a79a244a20e587cd2f08f6_205_0.png)

Figure 6.16 Classes that manage the functionality of service providers in Osp::Locations::Services.

# Osp::Media

Declared In:
FMedia.h

Library:
FMedia
