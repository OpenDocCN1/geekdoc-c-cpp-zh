

## VS Contoso Solution

Domain Objects

EntityFramework - Entity Configurations

The complete Domain model of this application can be represented in a UML diagram

GitHub: source

![](img/d73681d801b4b826e0b2a293897bbba4_235_0.png)

![](img/d73681d801b4b826e0b2a293897bbba4_235_1.png)

## Code First

The projects follow the Code First Entity Framework paradigm which means that there are no annotations or dependencies of the Domain Model to the Entity Framework. Instead the correlation between OOP entities and database entities is achieved using configuration files.

![](img/d73681d801b4b826e0b2a293897bbba4_236_0.png)

```
class StudentConfiguration : IEntityTypeConfiguration<Student>
{
    public void Configure(EntityTypeBuilder<Student> builder)
    {
        builder.Property(b => b.FirstName)
            .HasMaxLength(50);
        builder.Property(b => b.LastName)
            .HasMaxLength(50);
    }
}
```

GitHub: source

### 8.5.1 Repositories

The repositories are the contact point of the Domain with the outer layers. And it is at this point where we can use the functional structures of Option and Either. As you will see in most of the Repositories the Get operations have a similar signature:

```
Task<Option<T>> Get(int id)
```

For the methods that we want to retrieve a single element by its ID we could also use the Either in the case that we care about exposing any errors in the database.

```
public interface ICourseRepository
{
    Task<Option<Course>> Get(int id);
    Task<int> Add(Course course);
    Task<Unit> Update(Course course);
    Task<Unit> Delete(int id);
}
```

- Query operation: Get
- Command operations: Create, Update, Delete

GitHub: source

Also, the result is wrapped in a Task because in most cases the Persistence using Entity Framework 6 can be made asynchronous using Async methods for Save and Query. You can take a look at the Repositories implementations where the SaveChangesAsync and SingleOrDefaultAsync are used.

## 8.6 CQRS

The project uses the CQRS architectural pattern to reduce coupling. The term CQRS (Command Query Responsibility Segregation) is based on the famous CQS idea. It is the closest architecture available to split these responsibilities to accomplish more and simplify the design. It’s all about separating things, especially if they’re very different conceptually when it comes to reading and updating models.

The pattern basically divides into two categories:

- 1. Queries: get the information only, and never change anything within the model.
- 2. **Commands**: that’s when you perform the writes, updates, and deletes (along with all the logic’s complexities inherent to the business rules).

![](img/d73681d801b4b826e0b2a293897bbba4_238_0.png)

From the point of view of a web application HTTP Web API, the Queries would be the GET methods and the Commands would be POST/PUT/DELETE methods.

- 1. **Queries** - GET methods
- 2. **Commands** - POST/PUT/DELETE methods

Microsoft has the [CQRS pattern](CQRS pattern) listed as a part of the [Cloud design patterns](Cloud design patterns) and because of its rising usage, you can find reference in many of the Architecture guidance guides, for example in the .NET Microservices: *Architecture for Containerized .NET Applications* in the *Apply simplified CQRS and DDD patterns* chapter.

Of course CQRS can get complex inside large Domain Driven Architectures and Microsoft has provided some guides in the past like *Exploring CQRS and Event Sourcing* that are archived but maintain their value and worth exploring.

![](img/d73681d801b4b826e0b2a293897bbba4_239_0.png)

## 8.7 CQRS and MediatR

### 8.7.1 The Command Pattern with a Mediator

In the context of CQRS Commands and Queries are just DTOs (*Data transfer objects*) that encapsulate all the information needed to perform an action. For example:

```
public class CreateCourse : Record<CreateCourse>, IRequest<Either<Error, int>>
{
    public CreateCourse(string title, int credits, int departmentId)
    {
        Title = title;
        Credits = credits;
        DepartmentId = departmentId;
    }

    public string Title { get; }
    public int Credits { get; }
    public int DepartmentId { get; }
}
```

GitHub: source

In this project the CreateCourse DTO extends to two types:

- 1. is extending the Record<CreateCourse> class that belongs to the language extension library (Record<A>) and just provides Equals, IEquatable.Equals, IComparable.CompareTo, GetHashCode, operator==, operator!=, operator >, operator >=, operator <, and operator <= implementations for the class. This is not needed in this project but it is demonstrated as a good practice using the library.
- 2. Implements the IRequest<Either<Error, int>> interface that comes from the MediatR and allows the MediatR to find which object to use as a message. You can see the basic request/response pattern that MediatR uses here.

A powerful improvement can be made to the approach by decoupling the execution from the command state via the mediator pattern. In this pattern all commands, each of which consists of simple serializable state, are dispatched to the mediator and the mediator determines which handlers will execute the command:

![](img/d73681d801b4b826e0b2a293897bbba4_240_0.png)

Because the command is decoupled from execution it is possible to associate multiple handlers with a command and moving a handler to a different process space (for example splitting a Web API into multiple Web APIs) is simply a matter of changing the configuration of the mediator. And because the command is simple state we can easily serialize it into, for example, an event store (the example below illustrates a mediator that is able to serialize commands to stores directly, but this can also be accomplished through additional handlers).

Since commands are imperatives, they are typically named with a verb in the imperative mood (for example, "create" or "update"), and they might include the aggregate type, such as CreateOrderCommand. Unlike an event, a command is not a fact from the past; it is only a request, and thus may be refused.

It’s perhaps worth also briefly touching on the CQRS pattern – while the Command Message pattern may facilitate a CQRS approach it neither requires it nor has any particular opinion on it.

With that out of the way, let’s look at how this pattern impacts our application’s architecture.

Now inside each controller the Command message is sent immediately to the MediatR to be dispatched:

```
[Produces("application/json")]
[Route("api/[controller]")]
[ApiController]
public class CoursesController : ControllerBase
{
    private readonly IMediator _mediator;
    public CoursesController(IMediator mediator) => _mediator = mediator;

    [HttpGet("{courseId}")]
    public Task<IActionResult> Get(int courseId) =>
        _mediator.Send(new GetCourseById(courseId)).ToActionResult();
    ...
}
```

The MediatR send has this signature and just takes an IRequest<TResponse> request message:

```
Task<TResponse> Send<TResponse>(IRequest<TResponse> request, CancellationToken cancellationToken = default)
```

This is hooked to the receiving end to an IRequestHandler that has to implement a Handle(IRequest<TResponse> request) method.

![](img/d73681d801b4b826e0b2a293897bbba4_241_0.png)

```
public class CreateCourseAssignmentHandler : IRequestHandler<CreateCourseAssignment, Validation<Error, int>>
{
    private readonly IInstructorRepository _instructorRepository;
    private readonly ICourseRepository _courseRepository;
    private readonly ICourseAssignmentRepository _courseAssignmentRepository;

    public CreateCourseAssignmentHandler(IInstructorRepository instructorRepository,
        ICourseRepository courseRepository,
        ICourseAssignmentRepository courseAssignmentRepository)
    {
        _instructorRepository = instructorRepository;
        _courseRepository = courseRepository;
        _courseAssignmentRepository = courseAssignmentRepository;
    }

    public Task<Validation<Error, int>> Handle(CreateCourseAssignment request, CancellationToken cancellationToken) { ... }
}
```

We are going now to see in more detail the two basic paths Commands and Queries and how the language-ext functional style fits in.

### 8.7.2 Query Workflow

In this section we are going to see step by step the workflow of some of the Query paths. We will look at the GetCourseById case. We assume that we had an HTTP GET request from the client. This means that inside the CoursesController the Get(int courseId) action is called with the parameter courseId that was used in the HTTP request:

```
public class CoursesController : ControllerBase
{
    [HttpGet("{courseId}")]
    public Task<IActionResult> Get(int courseId) =>
        _mediator.Send(new GetCourseById(courseId)).ToActionResult();
    ...
}
```

As you can see, a message is immediately sent to the mediator. The message DTO (data transfer object) that is used here is GetCourseById:

```
public class GetCourseById : Record<GetCourseById>, IRequest<Option<CourseViewModel>>
{
    public GetCourseById(int courseId) => CourseId = courseId;
    public int CourseId { get; }
}
```

