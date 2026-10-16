

## VS Contoso 解决方案

领域对象

EntityFramework - 实体配置

该应用程序的完整领域模型可以用 UML 图表示。

GitHub：源代码

![](img/d73681d801b4b826e0b2a293897bbba4_235_0.png)

![](img/d73681d801b4b826e0b2a293897bbba4_235_1.png)

## Code First

这些项目遵循 Code First 的 Entity Framework 范式，这意味着领域模型没有对 Entity Framework 的注解或依赖。相反，OOP 实体与数据库实体之间的关联是通过配置文件实现的。

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

GitHub：源代码

### 8.5.1 仓储

仓储是领域与外层之间的接触点。正是在这一点上，我们可以使用 Option 和 Either 的函数式结构。正如你将看到的，在大多数仓储中，Get 操作都有相似的签名：

```
Task<Option<T>> Get(int id)
```

对于按 ID 检索单个元素的方法，如果我们关心暴露数据库中的任何错误，也可以使用 Either。

```
public interface ICourseRepository
{
    Task<Option<Course>> Get(int id);
    Task<int> Add(Course course);
    Task<Unit> Update(Course course);
    Task<Unit> Delete(int id);
}
```

- 查询操作：Get
- 命令操作：Create、Update、Delete

GitHub：源代码

此外，结果被包装在 Task 中，因为在大多数情况下，使用 Entity Framework 6 的持久化可以通过用于保存和查询的异步方法实现异步。你可以查看仓储实现，其中使用了 SaveChangesAsync 和 SingleOrDefaultAsync。

## 8.6 CQRS

该项目使用 CQRS 架构模式来降低耦合。CQRS（命令查询职责分离）这一术语基于著名的 CQS 思想。它是可用于拆分这些职责、实现更多目标并简化设计的最贴近的架构。这完全关乎分离事物，尤其是在读取和更新模型方面，这些概念在本质上有很大不同。

该模式基本分为两类：

- 1. 查询（Queries）：仅获取信息，绝不更改模型中的任何内容。
- 2. **命令（Commands）**：执行写入、更新和删除操作（以及业务规则中固有的所有逻辑复杂性）。

![](img/d73681d801b4b826e0b2a293897bbba4_238_0.png)

从 Web 应用程序 HTTP Web API 的角度来看，查询对应 GET 方法，命令对应 POST/PUT/DELETE 方法。

- 1. **查询** - GET 方法
- 2. **命令** - POST/PUT/DELETE 方法

微软将 [CQRS 模式](CQRS pattern) 列为 [云设计模式](Cloud design patterns) 的一部分，并且由于其使用日益广泛，你可以在许多架构指导指南中找到参考，例如在 .NET 微服务：*适用于容器化 .NET 应用程序的架构* 的 *应用简化的 CQRS 和 DDD 模式* 一章中。

当然，CQRS 在大型领域驱动架构中可能会变得复杂，微软过去也提供了一些指南，例如 *探索 CQRS 和事件溯源*，这些指南虽已归档，但仍具有价值，值得探索。

![](img/d73681d801b4b826e0b2a293897bbba4_239_0.png)

## 8.7 CQRS 与 MediatR

### 8.7.1 使用中介者的命令模式

在 CQRS 上下文中，命令和查询只是 DTO（*数据传输对象*），它们封装了执行操作所需的所有信息。例如：

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

GitHub：源代码

在这个项目中，CreateCourse DTO 扩展为两种类型：

- 1. 扩展了属于语言扩展库（Record<A>）的 Record<CreateCourse> 类，并为该类提供 Equals、IEquatable.Equals、IComparable.CompareTo、GetHashCode、operator==、operator!=、operator>、operator>=、operator< 和 operator<= 的实现。这个项目并不需要它，但展示了使用该库的良好实践。
- 2. 实现了来自 MediatR 的 IRequest<Either<Error, int>> 接口，允许 MediatR 找到要用作消息的对象。你可以在此处看到 MediatR 使用的基本请求/响应模式。

通过中介者模式将执行与命令状态解耦，可以对该方法进行强大的改进。在此模式中，所有命令（每个命令都包含简单的可序列化状态）都被分派给中介者，由中介者决定哪些处理程序将执行该命令：

![](img/d73681d801b4b826e0b2a293897bbba4_240_0.png)

由于命令与执行解耦，可以将多个处理程序与一个命令关联，并且将处理程序移动到不同的进程空间（例如将一个 Web API 拆分为多个 Web API）只需更改中介者的配置即可。而且由于命令是简单的状态，我们可以轻松地将其序列化到例如事件存储中（下面的示例说明了一个能够将命令直接序列化到存储中的中介者，但这也可以通过额外的处理程序来实现）。

由于命令是命令式的，它们通常使用祈使语气的动词命名（例如“create”或“update”），并且可能包含聚合类型，例如 CreateOrderCommand。与事件不同，命令不是过去的事实；它只是一个请求，因此可能会被拒绝。

也许还值得简要提及 CQRS 模式——虽然命令消息模式可能有助于 CQRS 方法，但它既不要求 CQRS，也没有对其有任何特定看法。

解决了这个问题后，让我们看看这种模式如何影响我们应用程序的架构。

现在，在每个控制器内部，命令消息会立即发送给 MediatR 以进行分派：

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

MediatR 的 Send 具有此签名，并且只接受一个 IRequest<TResponse> 请求消息：

```
Task<TResponse> Send<TResponse>(IRequest<TResponse> request, CancellationToken cancellationToken = default)
```

这在接收端连接到一个 IRequestHandler，该处理程序必须实现 Handle(IRequest<TResponse> request) 方法。

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

我们现在将更详细地了解命令和查询这两条基本路径，以及 language-ext 函数式风格是如何融入其中的。

### 8.7.2 查询工作流

在本节中，我们将逐步了解一些查询路径的工作流。我们将查看 GetCourseById 案例。我们假设客户端发出了一个 HTTP GET 请求。这意味着在 CoursesController 内部，会使用 HTTP 请求中使用的参数 courseId 调用 Get(int courseId) 操作：

```
public class CoursesController : ControllerBase
{
    [HttpGet("{courseId}")]
    public Task<IActionResult> Get(int courseId) =>
        _mediator.Send(new GetCourseById(courseId)).ToActionResult();
    ...
}
```

正如你所看到的，消息会立即发送给中介者。这里使用的消息 DTO（数据传输对象）是 GetCourseById：

```
public class GetCourseById : Record<GetCourseById>, IRequest<Option<CourseViewModel>>
{
    public GetCourseById(int courseId) => CourseId = courseId;
    public int CourseId { get; }
}
```

