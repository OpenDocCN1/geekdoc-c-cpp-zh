| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| InvokeMethod | TargetObject | manager | This is an instance of an OrderSystem class. |
|  | MethodName | ValidateOrder | A method on the OrderSystem class |
|  | Result | ValidationErrors | A variable that will be added to the workflow shortly |
|  | Parameters | theOrder | The instance of the Order class created by the GetOrderFromDropFile method above |

![](bbox=[0.13, 0.22, 0.53, 0.49])

# FIGURE 26-15

Next, the processing branches based on whether errors are encountered in the order. If the order is valid, then it is added to a collection for further processing. If, however, there are any validation errors, they are displayed and the workflow ends (see Figure 26-15). Set the properties for these activities as follows:

| ACTIVITY | PROPERTY | VALUE | DESCRIPTION |
|---|---|---|---|
| If | Condition | ValidationErrors.Length > 0 | The condition will return true if any errors were added to the collection by the earlier ValidateOrder call. |
| AddToCollection<T> | TypeArgument | OrderManager.Order | This defines the type of objects stored in the collection. |
|  | Collection | Orders | This is a variable of the workflow that will store the orders. |
|  | Item | theOrder | The item to add to the collection. In this case it is a workflow variable. |
| ForEach<T> | TypeArgument | String | This will iterate over each of the items in the ValidationErrors collection to display them. |
|  | Values | ValidationErrors | This is the collection to iterate over. |
| WriteLine | Text | ValidationError | This is the value of the current iteration in the loop. |
| TerminateWorkflow | Reason | "One or more orders have errors" | This will be available to the calling application to determine why the workflow terminated. |