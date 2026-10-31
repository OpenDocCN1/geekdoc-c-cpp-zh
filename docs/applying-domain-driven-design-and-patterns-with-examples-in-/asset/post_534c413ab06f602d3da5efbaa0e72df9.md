
## Class Table Inheritance [Fowler PoEAA]

> "Represents an inheritance hierarchy of classes with one table for each class."

[http://www.martinfowler.com/eeaCatalog/classTableInheritance.html](http://www.martinfowler.com/eeaCatalog/classTableInheritance.html)

## Coarse-Grained Lock [Fowler PoEAA]

> "Locks a set of related objects with a single lock."

http://www.martinfowler.com/eaaCatalog/coarseGrainedLock.html

## Collecting Parameter Pattern [Beck SBPP]

An object to pass to methods for collecting information from the methods.

## Data Mapper [Fowler PoEAA]

> "A layer of Mappers that moves data between objects and a database while keeping them independent of each other and the mapper itself."

[http://www.martinfowler.com/eaaCatalog/dataMapper.html](http://www.martinfowler.com/eaaCatalog/dataMapper.html)

## Data Transfer Objects [Fowler PoEAA]

> "An object that carries data between processes in order to reduce the number of method calls."

http://www.martinfowler.com/eaaCatalog/dataTransferObject.html

## Embedded Value [Fowler PoEAA]

> "Maps an object into several fields of another object's table."

[http://www.martinfowler.com/eaaCatalog/embeddedValue.html](http://www.martinfowler.com/eaaCatalog/embeddedValue.html)

## Entity [Evans DDD]

> "Many objects are not fundamentally defined by their attributes, but rather by a thread of continuity and identity."

[http://patternshare.org/default.aspx/Home.DDD.Entities](http://patternshare.org/default.aspx/Home.DDD.Entities)

## Factory [Evans DDD]

> "When creation of an object, or an entire aggregate, becomes complicated or reveals too much of the internal structure, factories provide encapsulation."

http://patternshare.org/default.aspx/Home.DDD.Factories

## Factory Method [GoF Design Patterns]

> "Define an interface for creating an object, but let subclasses decide which class to instantiate.
> Factory Method lets a class defer instantiation to subclasses."

## Foreign Key Mapping [Fowler PoEAA]

> "Maps an association between objects to a foreign key reference between tables."

[http://www.martinfowler.com/eaaCatalog/foreignKeyMapping.html](http://www.martinfowler.com/eaaCatalog/foreignKeyMapping.html)

## Generation Gap [Vlissides Pattern Hatching]

> "Modify or extend generated code just once no matter how many times it is regenerated."

http://www.research.ibm.com/designpatterns/pubs/gg.html

## Identity Field [Fowler PoEAA]

> "Saves a database ID field in an object to maintain identity between an in-memory object and a database row."

http://www.martinfowler.com/eaaCatalog/identityField.html

## Identity Map [Fowler PoEAA]

> "Ensures that each object gets loaded only once by keeping every loaded object in a map. Looks up objects using the map when referring to them."

http://www.martinfowler.com/eaaCatalog/identityMap.html

## Implicit Lock [Fowler PoEAA]

> "Allows framework or layer supertype code to acquire offline locks."

[http://www.martinfowler.com/eaaCatalog/implicitLock.html](http://www.martinfowler.com/eaaCatalog/implicitLock.html)

## Layer Supertype [Fowler PoEAA]

> "A type that acts as the supertype for all types in its layer."

http://www.martinfowler.com/eaaCatalog/layerSupertype.html

## Layers [POSA]

(Also in [Fowler PoEAA].)

> "Structures applications that can be decomposed into groups of subtasks in which each group of subtasks is at a particular level of abstraction."

[http://patternshare.org/default.aspx/Home.POSA.Layers](http://patternshare.org/default.aspx/Home.POSA.Layers)

## Lazy Load [Fowler PoEAA]

> "An object that doesn't contain all of the data you need but knows how to get it."

http://www.martinfowler.com/eaaCatalog/lazyLoad.html

## Metadata Mapping [Fowler PoEAA]

> "Holds details of object-relational mapping in metadata."

http://www.martinfowler.com/eaaCatalog/metadataMapping.html

## Model View Presenter [Fowler PoEAA2]

> "Separates the behavior of a presentation from the view while allowing the view to receive user events."

http://www.martinfowler.com/eaaDev/ModelViewPresenter.html

## Notification [Fowler PoEAA2]

> "An object that collects together information about errors and other information in the domain layer and communicates it to the presentation."

http://www.martinfowler.com/eaaDev/Notification.html

## Optimistic Offline Lock [Fowler PoEAA]

> "Prevents conflicts between concurrent business transactions by detecting a conflict and rolling back the transaction."

[http://www.martinfowler.com/eaaCatalog/optimisticOfflineLock.html](http://www.martinfowler.com/eaaCatalog/optimisticOfflineLock.html)

## Party Archetype [Arlow/Neustadt Archetype Patterns]

A way to represent information about people and organizations.

## Pessimistic Offline Lock [Fowler PoEAA]

> "Prevents conflicts between concurrent business transactions by allowing only one business transaction at a time to access data."

http://www.martinfowler.com/eaaCatalog/pessimisticOfflineLock.html

## Presentation Model [Fowler PoEAA2]

> "Represent the state and behavior of the presentation independently of the GUI controls used in the interface."

[http://www.martinfowler.com/eaaDev/PresentationModel.html](http://www.martinfowler.com/eaaDev/PresentationModel.html)

## Proxy [GoF Design Patterns]

> "Provides a surrogate or placeholder for another object to control access to it."

http://patternshare.org/default.aspx/Home.GOF.Proxy

## Query Object [Fowler PoEAA]

> "An object that represents a database query."

[http://www.martinfowler.com/eaaCatalog/queryObject.html](http://www.martinfowler.com/eaaCatalog/queryObject.html)

## Recordset [Fowler PoEAA]

> "An in-memory representation of tabular data."

http://www.martinfowler.com/eaaCatalog/recordSet.html

## Remote Façade [Fowler PoEAA]

> "Provides a coarse-grained façade on fine-grained objects to improve efficiency over a network."

[http://www.martinfowler.com/eaaCatalog/remoteFacade.html](http://www.martinfowler.com/eaaCatalog/remoteFacade.html)

## Repository [Evans DDD]

(Also in [Fowler PoEAA].)

An object for locating a certain Entity (or a set of Entities) that is in the middle of the life cycle.

[http://patternshare.org/default.aspx/Home.DDD.Repositories](http://patternshare.org/default.aspx/Home.DDD.Repositories)

## Separated Presentation [Fowler PoEAA2]

> "Ensure that any code that manipulates presentation only manipulates presentation, pushing all domain and data source logic into clearly separated areas of the program."

http://www.martinfowler.com/eaaDev/SeparatedPresentation.html

## Service Locator [Alur/Crupi/Malks Core J2EE Patterns]

> "Use a Service Locator to implement and encapsulate service and component lookup. A Service Locator hides the implementation details of the lookup mechanism and encapsulates related dependencies."

[http://www.corej2eepatterns.com/Patterns2ndEd/ServiceLocator.htm](http://www.corej2eepatterns.com/Patterns2ndEd/ServiceLocator.htm)

## Services [Evans DDD]

Responsibilities that don't naturally fit into Entities or Value Objects can be factored out to Services.

[http://patternshare.org/default.aspx/Home.DDD.Services](http://patternshare.org/default.aspx/Home.DDD.Services)
