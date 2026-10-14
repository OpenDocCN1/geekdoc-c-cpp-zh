```
CreateMappings();

var settings = new ApplicationSettings();
var taskService = new TaskServiceAdo(settings);
var objectMapper = new MapperAutoMapper();
controller = new TaskListController(taskService, objectMapper);
MainWindow = new TaskListView(controller);
MainWindow.Show();

controller.OnLoad();
}

private void CreateMappings()
{
    AutoMapper.Mapper.CreateMap<TaskDto, TaskViewModel>();
}

private TaskListController controller;
}
```

This code is the entry point to your application. The OnApplicationStartup method is an event handler that is called by internal WPF code to inform you that you can initialize things. In different types of applications, the entry point varies in style but is always a good place to put your dependency injection code.

The process of bootstrapping the application is very simple. The target is to construct a TaskListView, because that is the view class that acts as the resolution root of the application. Resolution roots are covered later in this chapter. In order to construct that class, you need a TaskListController instance. But that class requires both an ITaskService and an IObjectMapper, so you instantiate classes for both—this is where you are committing to the implementations. The TaskServiceAdo, in turn, requires an ISettings implementation, so you commit to the ApplicationSettings, which is an adapter for the ConfigurationManager .NET Framework class. Figure 9-3 clarifies this with a class diagram.