with the Ariba solution. Even worse, this user may have another account in Ariba, but due to the already initialized web session, is not able to log in accordingly.

Due to these special cases and also based on feedback indicating that people working on extension applications for those two solutions are typically not one and the same, SAP decided to establish the 1:1 account restriction rule for the time being.

Extension applications built with SAP HCP run in a managed standardized environment and have three core building blocks. Let's explore these elements in more detail.

# 11.2.1 Extension Application Frontend Layer

The vast majority of SAP HCP extension applications start “UI first” by creating a “clickable” UI mock. SAP clearly recommends using an SAP HCP HTML5 application for this layer. If you decide to leverage SAPUI5 as the UI technology for your extension, then you could also benefit from the SAP Web IDE. Particularly for SAPUI5, SAP HCP supports additional integration features as well, such as dynamic branding for SAP HANA Cloud Portal sites.

**What Is Dynamic Branding?**

One of the most commonly configured features in SAP on-premise products is to rebrand the product UIs in corporate colors and to place corporate logos. A few of the most notable publicly known brand color association examples are Coca-Cola™, with everything in the red spectrum, PepsiCo™, with everything predominantly blue, Shell in yellow, and LEGO™ in red. Because one of the requirements for extension applications is to integrate smoothly in the extended SAP solution like just another native module, branding is an essential part of that story. Therefore, by using SAP HANA Cloud Portal sites, an extension application has the opportunity to leverage dynamic branding and get automatically rethemed in the color scheme configured in the extended SAP Cloud solution.

Currently, this feature is only supported for SAPUI5-based applications, but depending on the customer or partner demand, support for dynamic branding may be extended toward other popular open-source UI frameworks.

The most commonly used approach to decouple the UI from the backend is via OData/JSON services. This also allows you to cleanly separate the UI development from the backend service development with a clean contract and reliable testing frame in between. Despite the widespread hype of cross-functional experts, practice shows that having specialized UI designers and skilled backend