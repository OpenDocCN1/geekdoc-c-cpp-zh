![](bbox=[0.14, 0.12, 0.88, 0.55])

# FIGURE 23.2

Big picture of the tool landscape.

The configuration model does not need to be changed when new revisions of master data are available within the source systems.

# 23.5 Data Integration

Applications can be connected to the catalog for gaining access to the product data. For example, a selector that does not require an inference engine but can directly work on the catalog data via implementing an API or using a web service. K-Build comes with the functionality to use product groups from the catalog as “branch-off points.” A branch-off point is treated like a component type, while being a pointer to a specific product group within the catalog. This means that the products belonging to the product group are treated like the possible child component types during run-time;