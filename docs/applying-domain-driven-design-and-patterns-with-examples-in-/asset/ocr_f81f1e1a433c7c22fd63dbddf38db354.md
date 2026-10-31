# Requirements on the Persistence Infrastructure

Let's repeat again that I want the infrastructure to stay out of the way of the Domain Model as much as possible so that I can focus on creating a powerful Domain Model for solving the business problem without having more distractions than are necessary. For example, I believe that I should be able to work with as high a level of Persistence Ignorance (PI) as possible, so that's a requirement of the infrastructure.

At the same time, it's also important not to put too much responsibility on the consumer of the Domain Model. I want to provide the consumer with a very simple API so that the consumer programmer can focus on what is important to him: creating a good experience for consumer users.

I have already defined certain desirable features for the life cycle of the persistent entities in Chapter 5, "Moving Further with Domain-Driven Design," but let's repeat it again here in Table 8-1.

# Table 8-1. Summary of the Semantics for the Life Cycle of the Domain Model Instances

| Operation | Result Regarding Transient/Persistent |
|---|---|
| Call to new | Transient |
| Repository.Add(instance) or persistentInstance.Add(instance) | Persistent in Domain Model |
| x.PersistAll() | Persistent in Database |
| Repository.Get() | Persistent in Domain Model (and Database) |
| Repository.Delete(instance) | Transient (and instance will get deleted from database at x.PersistAll) |

Another way of thinking about the requirements of the persistence infrastructure is to look at the non-functional requirements I have. Typical examples are scalability, security, and maintainability.

Of course, this varies widely, not only concerning the requirements, but also because a certain persistence framework can sometimes fail and sometimes succeed for the same mix of non-functional requirements. The reason for this is that the success or failure depends on the type of application, the usage patterns, and so on. I have to leave it up to the reader to define her own mix of non-functional requirements and to check whether a certain persistence framework can fulfill the requirements by carrying out careful tests. Just remember that if your appetite for non-functional requirements becomes too big, it will cost you a lot somewhere else.