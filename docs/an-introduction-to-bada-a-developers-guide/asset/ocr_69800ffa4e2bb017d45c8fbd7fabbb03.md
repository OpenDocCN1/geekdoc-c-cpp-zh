Namespaces used:
Osp::Locations::Services, Osp::Locations::Controls, Osp::Graphics

Header files to #include:
FLocations.h

Required libraries:
FLocations, LocationControls

Required privilege level:
Normal

Required privilege groups:
LOCATION, LOCATION_SERVICE

The namespace Osp::Locations::Services provides a number of useful services that can be exploited by the developer. An essential service that we will also introduce is what is encapsulated in the IMapServiceProvider interface.

A further namespace used in this recipe is Osp::Locations::Controls, which allows users to pan, zoom and interact with maps as is generally expected.

We simply show how a map can be displayed on screen. Our sample code presents snippets from a C++ source file and its corresponding header file, which we called MapVisualisation.cpp (covers code for presenting geographic data as a map).

In order to be able to display maps we need access to a geographic data provider. For this example we use deCarta as our map provider. You can sign up at the deCarta website (developer.decar ta.com) and request a key for free.

Once you have your key, you can link your deCarta account in the application by creating a map provider object. We do this in our MapVisualisation class.

```
// Define a name for the provider
String providerName = L"deCarta";

// Set a map key for deCarta (insert your username/pwd instead of XXX/
// YYY)
static const String extraInfo = L"ClientName=XXX;ClientPassword=YYY;"
"HostUrl=http://developer.kr.dz.decarta.com:80/openls/openls";

// Create a map provider
IMapServiceProvider* pProvider = static_cast<IMapServiceProvider*>(
ProviderManager::ConnectToServiceProviderN(L"deCarta",
LOC_SVC_PROVIDER_TYPE_MAP, extraInfo));
```