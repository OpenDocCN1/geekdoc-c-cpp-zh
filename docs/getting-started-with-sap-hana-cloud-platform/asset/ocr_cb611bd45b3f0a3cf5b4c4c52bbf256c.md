can specify the target JTA data source that you want to use to define your persistence unit. Here, the data source name is defined in terms of the JNDI data source name assigned whenever a schema binding is created. If this element is omitted, then the default data source for the application is used implicitly.

+   4. The next section is used to identify the entity classes that will be included in the persistence unit. Here, you have the choice of plugging in the fully qualified class names of annotated entity classes or pointing to a separate XML-based ORM mapping file. In the former case, this listing is usually optional, because most persistence providers are able to detect the presence of entity classes automatically.

+   5. Lastly, within the `<properties>` element, you can specify custom properties that configure the JPA persistence provider, the underlying JDBC-based data source, or both. In the example file contained in Listing 6.4, we've specified a custom property of the EclipseLink persistence provider called `eclipselink.ddl-generation`. This property coerces EclipseLink into automatically creating database tables based on the defined entities contained within the persistence unit at deployment time. As you can imagine, this property comes in quite handy when it comes time to transport applications.

```
<persistence>
  <persistence-unit name="examplePU" transaction-type="JTA">
    <provider>
      <!-- Class name of persistence provider -->
      org.eclipse.persistence.jpa.PersistenceProvider
    </provider>

    <!-- Entity Classes/ORM Mapping Files Section -->
    <class>com.sappress.hcbook.ch06.Persistence.Incident</class>
    <class>...</class>

    <!--mapping-file>META-INF/orm.xml</mapping-file>-->

    <!-- Custom Properties Section -->
    <properties>
      <property name="eclipselink.ddl-generation"
        value="create-tables" />
    </properties>
  </persistence-unit>
</persistence>
```

# Listing 6.4 Defining a Persistence Unit