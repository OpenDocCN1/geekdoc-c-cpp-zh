There are two very different dependencies here: NHibernate is used for commands, and MongoDB is used for queries. The former is an Object/Relational Mapper used here for storing a domain model. The latter is a document storage library used for fast querying. This class has two disparate dependencies and therefore two reasons to change. With such different dependencies, it is likely that their respective decorators will also be different. Rather than being split into very small operations, as the entire CRUD interface was earlier in this chapter, this interface will only be split into two parts: commands and queries. Figure 10-3 shows a UML class diagram of how this will be orchestrated.

With the commands and queries split between two interfaces, the implementations can depend on different packages. The commands implementation will depend only on NHibernate, and the queries implementation will depend only on MongoDB.

![](bbox=[0.157, 0.275, 0.892, 0.557])

**FIGURE 10-3** Splitting interfaces by architectural need allows implementations to have very different dependencies.

Ideally, these two implementations will not only be different classes, but those classes will reside in different packages—assemblies—too. If not, the problem is only partially alleviated because it will be impossible to reuse one implementation without depending on the other, plus the chain of dependencies—the NHibernate or Mongo libraries—that comes with it.

Listing 10-33 shows the interfaces after they have been split. The two can now be implemented separately.

**LISTING 10-33** The interface has been split into query and command methods.

```
public interface IPersistenceQueries
{
    IEnumerable<Item> GetAll();

    Item GetByID(Guid identity);

    IEnumerable<Item> FindByCriteria(string criteria);
}
```