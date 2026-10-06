
```
foreach (var relationship in builder.Model.GetEntityTypes()
    .SelectMany(e => e.ForeignKeys()))
{
    relationship.DeleteBehavior = DeleteBehavior.Restrict;
}
}
```

### 创建表

要向数据库添加表，你必须创建一个新的迁移并更新数据库。

- 1. 打开程序管理器控制台，在右侧下拉菜单中选择 `VideoOnDemand.Data`。
- 2. 执行以下命令创建迁移：  
  `add-migration CreateVideoRelatedTables`
- 3. 执行以下命令将迁移更改应用到数据库：  
  `update-database`

# 初学者 ASP.NET Core MVC & Razor Pages

## 添加种子数据 (Seed Data)

为了在表创建后有数据可用，你将在表创建后向它们添加种子数据。你需要在 Data 文件夹中添加一个名为 `DbInitializer` 的类来添加种子数据。

种子数据通过名为 `Initialize` 的静态方法添加，你需要将该方法添加到类中。

如果你希望每次应用迁移（migrations）时都重建数据库，可以在 `Initialize` 方法的开头添加以下行代码。这在某些需要干净数据库的测试场景中非常有用。本次练习中不会添加它们，因为你希望在迁移之间保留已添加的数据。

```
context.Database.EnsureDeleted();
context.Database.EnsureCreated();
```

向表中添加数据，你需要创建一个实体类型的列表并添加实例。然后使用传递给 `Initialize` 方法的上下文对象，将其添加到 `VODContext` 类中的实体集合（该实体的 `DbSet`）中。

注意添加种子数据的顺序很重要，因为某些表可能与其他表关联，并且需要那些表的主键。

- 右键点击 `VideoDemand.Data` 项目并选择“设为启动项目”（Set as Startup Project）。
- 在 Migrations 文件夹中添加一个名为 `DbInitializer` 的类。
- 为类添加一个名为 `RecreateDatabase` 的公共静态方法。它应该接收 `VODContext` 作为参数。如果需要重建数据库，可以调用此方法；重建时整个数据库中的所有数据都将被删除。

```
public static void RecreateDatabase(VODContext context)
{
```

- 在上下文对象上调用 `EnsureDeleted` 和 `EnsureCreated` 方法以删除数据库并创建一个新的。
`context.Database.EnsureDeleted();`
`context.Database.EnsureCreated();`

- 5. 在类中添加一个名为 `Initialize` 的公共静态方法。它应该接收 `VODContext` 作为参数。

```
public static void Initialize(VODContext context)
{
}
```

- 6. 为了避免重复虚拟数据，将添加一个包含 Lorem 文本的变量，该变量可以在整个种子过程中复用。你可以在以下 URL 生成 Lorem 文本：http://loripsum.net/
`var description = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tincidunt incididunt ut labore et dolore magna aliqua. Ut enim minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea consequat;";`

- 7. 添加三个用于存储邮箱、管理员角色和用户 ID 的变量。这些变量将在整个 `Initialize` 方法中使用。邮箱地址应存在于 `AspNetUsers` 表中；如果不在，请添加具有该邮箱地址的用户，或更改该值以向表中添加邮箱地址。该用户将是管理员；如果不是，请添加 `AspNetRoles` 表并使用用户 ID 和 `RoleId` 列中的 `1` 添加一条记录。

```
var email = "@b.c";
var adminRoleId = string.Empty;
var userId = string.Empty;
```

- 8. 尝试使用 `Users` 实体从 `AspNetUsers` 表中获取用户。

```
if (context.Users.Any(r => r.Email.Equals(email)))
    userId = context.Users.First(r => r.Email.Equals(email)).Id;
```

- 9. 添加一个 `if` 块来检查用户是否成功获取。所有剩余代码都应该放在此 `if` 块内部。

```
if (!userId.Equals(string.Empty))
{}
```

- 10. 使用 `Instructors` 实体在未添加数据的情况下，向数据库中的 `Instructors` 表添加导师数据。

```c
if (!context.Instructors.Any())
{
    var instructors = new List<Instructor>
    {
        new Instructor {
            Name = "John Doe",
            Description = description.Substring(20, 50),
            Thumbnail = "/images/Ice-Scrat-icon.png"
        },
        new Instructor {
            Name = "Jane Doe",
            Description = description.Substring(30, 40),
            Thumbnail = "/images/Ice-Scrat-icon.png"
        }
    };
    context.Instructors.AddRange(instructors);
    context.SaveChanges();
}
```

- 11. 使用该实体在未添加数据的情况下，向数据库中的 `Courses` 表添加课程数据。

```c
if (!context.Courses.Any())
{
    var instructorId = context.Instructors.First().Id;
    var instructorId2 = int.MinValue;
    var instructor = context.Instructors.Skip(1).FirstOrDefault();
    if (instructor != null) instructorId2 = instructor.Id;
    else instructorId2 = instructorId;
    var courses = new List<Course> {
        new Course {
            InstructorId = instructorId,
            Title = "Course 1",
            Description = description,
            ImageUrl = "/images/course.jpg",
            MarImageUrl = "/images/laptop.jpg"
        },
        new Course {
            InstructorId = instructorId2,
            Title = "Course 2",
            Description = description,
            ImageUrl = "/images/course1.jpg",
            MarImageUrl = "/images/laptop.jpg"
        },
        new Course {
            InstructorId = instructorId1,
            Title = "Course 3",
            Description = description,
            ImageUrl = "/images/course3.jpg",
            MarImageUrl = "/images/laptop.jpg"
        }
    };
    context.Courses.AddRange(courses);
    context.SaveChanges();
}
```

- 12. 从新添加的课程中获取 ID。这些 ID 将在其他表中引用。

```c
var courseId1 = int.MinValue;
var courseId2 = int.MinValue;
var courseId3 = int.MinValue;
if (context.Courses.Any())
{
    courseId1 = context.Courses.First().Id;
    courseId2 = context.Courses.Skip(1).FirstOrDefault()?.Id ?? courseId1;
    courseId3 = context.Courses.Skip(2).FirstOrDefault()?.Id ?? courseId2;
}
```

- 13. 使用 `UserCourses` 实体连接用户和课程。

```c
if (!context.UserCourses.Any())
{
    context.UserCourses.AddRange(new List<UserCourse>
    {
        new UserCourse { UserId = userId, CourseId = courseId1 },
        new UserCourse { UserId = userId, CourseId = courseId2 },
        new UserCourse { UserId = userId, CourseId = courseId3 }
    });
    context.SaveChanges();
}
```

- 14. 使用 `Modules` 实体在未添加数据的情况下，向 `Modules` 表添加模块数据。

```c
if (!context.Modules.Any())
{
    var modules = new List<Module>
    {
        new Module { CourseId = courseId1, Title = "Module 1" },
        new Module { CourseId = courseId2, Title = "Module 2" },
        new Module { CourseId = courseId3, Title = "Module 3" }
    };
    context.Modules.AddRange(modules);
    context.SaveChanges();
}
```

- 15. 从新添加的模块中获取 ID。这些 ID 将在其他表中引用。

```c
var moduleId1 = int.MinValue;
var moduleId2 = int.MinValue;
var moduleId3 = int.MinValue;
if (context.Modules.Any())
{
    moduleId1 = context.Modules.First().Id;
    moduleId2 = context.Modules.Skip(1).FirstOrDefault()?.Id ?? moduleId1;
    moduleId3 = context.Modules.Skip(2).FirstOrDefault()?.Id ?? moduleId2;
}
```

- 16. 使用 `Videos` 实体在未添加数据的情况下，向 `Videos` 表添加视频数据。

```c
if (!context.Videos.Any())
{
    var videos = new List<Video>
    {
        new Video {
            ModuleId = moduleId1,
            Title = "Video 1",
            Description = description.Substring(0, 50),
            ImageUrl = "/images/video.jpg",
            MarImageUrl = "/images/laptop.jpg"
        },
        new Video {
            ModuleId = moduleId2,
            Title = "Video 2",
            Description = description.Substring(50, 50),
            ImageUrl = "/images/video2.jpg",
            MarImageUrl = "/images/laptop.jpg"
        },
        new Video {
            ModuleId = moduleId3,
            Title = "Video 3",
            Description = description.Substring(100, 50),
            ImageUrl = "/images/video3.jpg",
            MarImageUrl = "/images/laptop.jpg"
        }
    };
    context.Videos.AddRange(videos);
    context.SaveChanges();
}
```

# 初学者 ASP.NET Core 2.0 MVC & Razor Pages

```
context.Downloads.AddRange(downloads);
context.SaveChanges();
}
```
