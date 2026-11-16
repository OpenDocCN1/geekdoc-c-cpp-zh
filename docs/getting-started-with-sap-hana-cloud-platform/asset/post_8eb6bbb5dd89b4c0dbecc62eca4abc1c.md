
respectively. Using these annotations (and their corresponding attributes), you can specify foreign key relationships, relationship cardinalities, cascading behaviors (e.g., delete all children whenever the parent is deleted), and so forth.

```
public class Incident {
    @Id
    private String id;
    @Basic
    private String title = "";

    ...

    @OneToOne(cascade=CascadeType.PERSIST)
    @JoinColumn(name="LOCATION_ID", referencedColumnName="ID")
    private Location location = new Location();

    @OneToMany(mappedBy="incident", cascade=CascadeType.ALL)
    private List<InvolvedPerson> involvedPersons =
        new ArrayList<InvolvedPerson>();

    ...
}
```

### Listing 6.3 Defining Relationships between Entities

After all of the relevant entities are defined, the next step is to group them all together in something the JPA calls a persistence unit. Persistence units are defined within a specialized XML file called persistence.xml. This XML file provides the JPA with a logical grouping of entity classes and with lower-level database configuration details.

Listing 6.4 illustrates the basic anatomy of a persistence.xml file. Here, configuration details are organized into specific sections:

- 1. Within the <persistence-unit> element, you must specify the name of your persistence unit and the transaction type. In managed environments such as SAP HCP, the Java Transaction API (JTA) option will be used by default.
- 2. Next, use the <provider> element to inform the JPA which persistence provider you plan to use. Here, you must plug in the fully qualified class name of a JPA persistence provider class. In the example shown in Listing 6.4, we've proposed the popular EclipseLink persistence provider. EclipseLink is generally the preferred persistence provider used within SAP HCP.
- 3. Although not depicted in Listing 6.4, the next element in the persistence schema is the optional <jta-data-source> element. Within this element, you can specify the target JTA data source that you want to use to define your persistence unit. Here, the data source name is defined in terms of the JNDI data source name assigned whenever a schema binding is created. If this element is omitted, then the default data source for the application is used implicitly.
- 4. The next section is used to identify the entity classes that will be included in the persistence unit. Here, you have the choice of plugging in the fully qualified class names of annotated entity classes or pointing to a separate XML-based ORM mapping file. In the former case, this listing is usually optional, because most persistence providers are able to detect the presence of entity classes automatically.
- 5. Lastly, within the `<properties>` element, you can specify custom properties that configure the JPA persistence provider, the underlying JDBC-based data source, or both. In the example file contained in Listing 6.4, we've specified a custom property of the EclipseLink persistence provider called `eclipselink.ddl-generation`. This property coerces EclipseLink into automatically creating database tables based on the defined entities contained within the persistence unit at deployment time. As you can imagine, this property comes in quite handy when it comes time to transport applications.

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

### Listing 6.4 Defining a Persistence Unit

As you can imagine, this brief introduction barely scratches the surface with regards to the myriad of ORM options available within JPA. For a more comprehensive reference, we highly recommend that you pick up a copy of Java Persistence with JPA 2.1 (Yang, Outskirts Press, 2013). You can also find details concerning specific annotation types in the Java EE 6 API documentation online at http://docs.oracle.com/javaee/6/api.

## Manipulating Entities Programmatically

In terms of development effort, mapping entities for use within the JPA is by far the hardest part. Once the entities are defined, JPA makes it easy to access and manipulate entity instances at runtime. Here, you need only obtain a javax.persistence.EntityManager instance, and you’re off and running.

Within a managed environment like SAP HCP, EntityManager instances are normally obtained via dependency injection inside of a stateless session bean, as shown in Listing 6.5. This approach allows you to take advantage of the container-managed persistence (CMP) capabilities of the Java EE application container. Here, you allow the application container to manage the lifecycle of the entity manager and the transactions you perform against it.

```
import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;

@Stateless
@LocalBean
public class IncidentBean {
    @PersistenceContext private EntityManager em;
    ...
}
```

### Listing 6.5 Obtaining a JPA Entity Manager Instance via Injection

Because injection ensures that the EntityManager instance is created during the bean-allocation process, you can begin using it to perform CRUD operations in EJB business methods right away. For example, in Listing 6.6, you can see how we’re using the persist() method of the EntityManager interface to create a new incident record. In this scenario, the Incident instance (which is basically just a POJO) was instantiated using the new operator and populated via a series of setter methods, just like any other Java object. When passed to the persist() method, though, the Incident instance becomes a managed entity instance—at least for the duration of the JTA transaction spawned by the EJB container. After the addIncident() method completes, the JTA transaction is automatically committed, and the entity instance becomes “detached.” This is to say that the Incident instance effectively becomes a normal object that can be passed around via different application layers without fear of thread safety or transactional integrity issues.

```
public class IncidentBean {
public Incident addIncident(Incident incident) {
return em.persist(incident);
}
}
```

### Listing 6.6 Creating Entity Records Using the JPA

After an entity record is created, you can update it using the merge() method of the EntityManager interface, as shown in Listing 6.7. As the method name suggests, this method effectively merges the state of the passed entity object with the persistence context.

```
public class IncidentBean {
public Incident updateIncident(Incident incident) {
return em.merge(incident);
}
}
```

### Listing 6.7 Updating Entity Records Using the JPA

To delete an entity record, you can use the remove() method of the EntityManager interface. However, as you can see in Listing 6.8, there is a twist calling this method. Before you can remove a detached entity, you must first merge it into the persistence context. Therefore, first you merge the entity using merge(), and then you can simply pass the result on to remove().

```
public class IncidentBean {
public void removeIncident(Incident incident) {
em.remove(em.merge(incident));
}
}
```

### Listing 6.8 Deleting Entity Records Using the JPA

When it comes to fetching entity instances, you have one of two options:

- If you happen to know the primary key of the target entity record, you can use the find() method of the EntityManager interface to look it up.
- For more advanced lookups, you can utilize a SQL-like query language called JPA Query Language (JPQL) to process queries.

Listing 6.9 demonstrates how the find() method is used to lookup an entity record by its primary key. Here, you must pass in two parameters: the entity class and the primary key, which can be of any object type in order to support composite keys.

```
public class IncidentBean {
    public Incident getIncidentById(String id) {
        return em.find(Incident.class, id);
    }
}
```

### Listing 6.9 Fetching an Entity Record via Its Primary Key

If you have the primary key of an entity in hand, then the find() method is by far the easiest and most efficient way to go. More often than not, though, you probably won't know the primary key. This is particularly true of database schemas that utilize the autogeneration of keys. In these scenarios, you can create ad hoc queries using JPQL to find entity records based on alternative selection criteria. For example, in Listing 6.10, you can see how we're using JPQL to search for incident records created from a given date up until now. Here, you can use the createQuery() method of the EntityManager instance to define the query and then parameterize the query and execute it. Notice that the result set comes back as a series of entities wrapped up in a java.util.List collection. Naturally, the entities within the collection are detached and can be passed between different application layers as needed.

```
public class IncidentBean {
    public List<Incident> getIncidentsByDate(Date fromDate) {
        TypedQuery<Incident> query =
            em.createQuery("SELECT i FROM Incident i WHERE i.ReportedOn BETWEEN ?1 and ?2.",
            Incident.class);
        query.setParameter(1, fromDate);
        query.setParameter(2, new Date(System.currentTimeMillis()));
        return query.getResultList();
    }
}
```

### Listing 6.10 Using JPQL to Search for Entity Records
