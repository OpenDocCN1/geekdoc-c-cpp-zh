This snippet shows some of the main terms you will see repeatedly throughout your work with the Entity Framework. The EntityType defines one of your objects — in this case, the author class. The collection of authors is defined as an EntitySet. There are AssociationSets that define the relationships between the various EntityTypes. Finally, there is an EntityContainer that groups everything. One point to notice is that each of the Property elements in the XML file has a Type attribute. This attribute uses Visual Basic data types, rather than database-specific types. This XML file will be updated as you change your conceptual model.

If you look at one of the generated types in the Class View window (see Figure 11-9), you will see that it inherits from EntityObject. The EntityObject class in turn inherits from StructuralObject and implements three interfaces (IEntityWithChangeTracker, IEntityWithKey and IEntityWithRelationships). The names of these three interfaces give you some idea of what the generated classes are capable of:

+   - They are able to identify one another via one or more key properties.
+   - They are aware of changes to their properties; therefore, you will be able to identify changed objects and/or properties without requiring a trip back to the database.
+   - They track their relationship to one or more other EntityObjects.

# Storage Model

The storage model XML initially looks similar to the conceptual model XML (see the generated PubsModel .ssdl file in the Solution Explorer View):

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<Schema Namespace="PubsModel.Store" Alias="Self" Provider="System.Data.SqlClient" ProviderManifestToken="2008" xmlns:store="http://schemas.microsoft.com/ado/2007/12/edm/EntityStoreSchemaGenerator" xmlns="http://schemas.microsoft.com/ado/2009/02/edm/ssdl">
  <EntityContainer Name="PubsModelStoreContainer">
    <EntitySet Name="authors" EntityType="PubsModel.Store.authors" store:Type="Tables" Schema="dbo" />
    <EntitySet Name="titleauthor" EntityType="PubsModel.Store.titleauthor" store:Type="Tables" Schema="dbo" />
    <EntitySet Name="titles" EntityType="PubsModel.Store.titles" store:Type="Tables" Schema="dbo" />
    <AssociationSet Name="FK__titleauth__au_id__0CBAE877" Association="PubsModel.Store.FK__titleauth__au_id__0CBAE877">
      <End Role="authors" EntitySet="authors" />
      <End Role="titleauthor" EntitySet="titleauthor" />
    </AssociationSet>
    <AssociationSet Name="FK__titleauth__title__0DAF0CB0" Association="PubsModel.Store.FK__titleauth__title__0DAF0CB0">
      <End Role="titles" EntitySet="titles" />
      <End Role="titleauthor" EntitySet="titleauthor" />
    </AssociationSet>
  </EntityContainer>
  <EntityType Name="authors">
```
```

![](bbox=[0.649, 0.088, 0.881, 0.369])

![](bbox=[0.693, 0.401, 0.881, 0.568])