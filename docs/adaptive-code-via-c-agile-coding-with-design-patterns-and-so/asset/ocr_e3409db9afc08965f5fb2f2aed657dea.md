![](bbox=[0.17, 0.006, 0.82, 0.31])

FIGURE 9-1 The task list has some state beyond the task description: priority, due date, and the task’s completion state.

Because this is a WPF application, you are using the Model-View-ViewModel (MVVM) pattern to ensure a separation of concerns between the layers. The application strives to use best practices—although dependency injection is still to come. One of the view models is the backing controller for the main window. TaskListController delegates to a TaskService to retrieve all of the tasks. An example of how this is currently accomplished without dependency injection is shown in Listing 9-1.

# LISTING 9-1 This controller does not use dependency injection.

Click here to view code image

```
{
    public event PropertyChangedEventHandler PropertyChanged = delegate {};

    private readonly ITaskService taskService;
    private readonly IObjectMapper mapper;
    private ObservableCollection<TaskViewModel> allTasks;

    public TaskListController()
    {
        this.taskService = new TaskServiceAdo();
        this.mapper = new MapperAutoMapper();

        var taskDtos = taskService.GetAllTasks();
        AllTasks = new ObservableCollection<TaskViewModel>(mapper.Map<IEnumerable<TaskViewModel>>(taskDtos));
    }
```