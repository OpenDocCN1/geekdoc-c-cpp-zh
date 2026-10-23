# SIEMENS: Configuration and Reconfiguration in Industry

Andreas Falkner and Herwig Schreiner

Siemens AG Österreich, Vienna, Austria

Abstract: Whereas the configuration of consumer products such as PCs, cars, insurances, and such is well understood and supported by commercial tools, large-scale industrial systems still raise considerable challenges concerning modeling, solving, and performance. After a short explanation of the importance of this topic to Siemens, this chapter presents the domain of railway interlocking systems as an example of such complex industrial systems and discusses detailed requirements for their configuration. It then reports on techniques used for solving those requirements at Siemens as well as on results of their application.

# 16.1 Introduction

Siemens¹ is a global company that produces a rich variety of products in its four sectors, Energy, Industry, Healthcare, and Infrastructures and Cities, from relatively small items (such as electric power supplies, gear units, etc.) to very complex items (such as power plants, gas turbines, railway interlocking systems, etc.). Many of these products are configurable, either by a Siemens engineer or sales manager who prepares a bid, or directly by a business customer who selects components or features before buying the product.

Depending on the special requirements of the products and production processes, Siemens uses different configurators, some tailor-made (such as Siemens Industry Mall), some using configurators built into Siemens’ product life-cycle management tools COMOS and Teamcenter, and some based on external commercial tools (such as SAP’s Variant Configurator or Internet Pricing Configurator²).

None of those tools was available or well suited for the task of configuring a new type of Siemens railway interlocking system developed in the 1990s. The challenge was to move from an engineer-to-order type of process (suitable for traditional relay interlockings) to a configure-to-order process in order to reduce costs for the new type of electronic interlockings. This posed the following challenges for the configuration system:

+   - High variability: Many different component types and subtypes (hundreds of types, thousands of attributes), different variants for different countries

+   - Dynamic data: The number of components is not fixed but is derived only during the configuration process