```
<Key>
  <PropertyRef Name="au_id" />
</Key>
<Property Name="au_id" Type="varchar" Nullable="false" MaxLength="11" />
<Property Name="au_lname" Type="varchar" Nullable="false" MaxLength="40" />
<Property Name="au_fname" Type="varchar" Nullable="false" MaxLength="20" />
<Property Name="phone" Type="char" Nullable="false" MaxLength="12" />
<Property Name="address" Type="varchar" MaxLength="40" />
<Property Name="city" Type="varchar" MaxLength="20" />
<Property Name="state" Type="char" MaxLength="2" />
<Property Name="zip" Type="char" MaxLength="5" />
<Property Name="contract" Type="bit" Nullable="false" />
</EntityType>
...
```

Code snippet from SimpleEF

One major difference between this file and the earlier conceptual model is that the types in the storage model are SQL Server data types. In addition, unlike the conceptual model file, this file will not change as you update your Entity Framework model, as it is tied to the database structure.

# Mapping Model

Finally, you have the third XML file, the mapping schema language (MSL) file:

```
<?xml version="1.0" encoding="utf-8"?>
<Mapping Space="C-S" xmlns="http://schemas.microsoft.com/ado/2008/09/mapping/cs">
  <EntityContainerMapping StorageEntityContainer="PubsModelStoreContainer" CdmEntityContainer="PubsEntities">
    <EntitySetMapping Name="authors">
      <EntityTypeMapping TypeName="PubsModel.author">
        <MappingFragment StoreEntitySet="authors">
          <ScalarProperty Name="au_id" ColumnName="au_id" />
          <ScalarProperty Name="au_lname" ColumnName="au_lname" />
          <ScalarProperty Name="au_fname" ColumnName="au_fname" />
          <ScalarProperty Name="phone" ColumnName="phone" />
          <ScalarProperty Name="address" ColumnName="address" />
          <ScalarProperty Name="city" ColumnName="city" />
          <ScalarProperty Name="state" ColumnName="state" />
          <ScalarProperty Name="zip" ColumnName="zip" />
          <ScalarProperty Name="contract" ColumnName="contract" />
        </MappingFragment>
      </EntityTypeMapping>
    </EntitySetMapping>
  ...
```

Code snippet from SimpleEF

This may seem like a great deal of overhead, as it appears to map properties of the classes to the identical fields of tables. However, as you customize the conceptual model, the mapping model will change to reflect the new structure. As the Entity Framework supports mapping a single object to multiple tables, or vice versa, this mapping model increases in importance, and is the core benefit of using a framework such as Entity Framework.

# LINQ to Entities

Just as there is LINQ to SQL, LINQ to XML, and LINQ to objects, there is also a LINQ syntax for working with Entity Framework models. The syntax is very similar to that used by LINQ to SQL, in that a context object is used as your access point to the exposed classes. You first create an instance of that context