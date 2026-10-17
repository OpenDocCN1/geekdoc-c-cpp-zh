
## 处理日历项目的内容

要处理日历项目的内容，请设置或获取相应的属性。这些广泛使用的属性：

- `Subject` 是预约的主题。
- `Body` 是预约的正文内容。
- `Start` 是预约的开始时间。
- `End` 是预约的结束时间。
- `BusyStatus` 是您在预约期间的状态：`olBusy`、`olFree`、`olOutOfOffice` 或 `olTentative`。
- `Categories` 是分配给项目的类别或多个类别。
- `ReminderSet` 决定预约是否有提醒（True）或无提醒（False）。
- `ReminderBeforeStart` 是提醒在事件发生前的几分钟。

以下示例创建了一个新的 `Appointment` 对象并将其赋值给对象变量 `myAppointment`。它设置了主题、正文、开始日期（当前日期后 7 天的下午 2:30）和结束日期（开始一小时后）；将时间标记为忙碌；分配了“个人”类别；设置在预约前 30 分钟提醒；并保存了它：

```
Dim myAppointment As AppointmentItem

Set myAppointment = Application.CreateItem(ItemType:=olAppointment)

myAppointment.Subject = "Dentist"

With myAppointment

  .Body = "Dr. Schmitt " & vbCr & "4436 Acacia Blvd."

  .Start = Str(Date + 7) & "2.30 PM"

  .End = Str(Date + 7) & "3.30 PM"

  .BusyStatus = olBusy

  .Categories = "Personal"

  .ReminderMinutesBeforeStart = 30

  .ReminderSet = True

  .Save

  End With
```

`AppointmentItem` 对象总共有 71 个属性。如果您想探索更多属性，请查看此 MSDN 网页页：

`http://msdn.microsoft.com/en-us/library/office/jj990814.aspx`

## 允许用户手动分配类别

通过程序化为项目分配类别可能是困难的，特别是因为许多用户会以独特的方式创建自定义类别或分配类别。在许多情况下，通过在过程的适当时点显示类别对话框，让每个用户手动分配他们偏好的类别会更好。您可以通过使用项目的 `ShowCategoriesDialog` 方法来实现——对于由对象变量 `myAppointment` 引用的项目，使用 `myAppointment.ShowCategoriesDialog`。

## 处理任务和任务请求

VBA 可以自动化任务和任务请求。以下章节将向您展示如何创建任务、处理任务内容以及发送任务请求。

### 创建任务

创建一个新的任务项目项，请使用 `Application` 对象的 `CreateItem` 方法并在 `ItemType` 参数中指定 `olTaskItem`。以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTaskItem)
```

### 处理任务项目的内容

要处理任务项目的内容，请设置或获取相应的属性。这些是最实用的属性：

- `Subject` 是任务的主题。
- `Body` 是任务的正文内容。
- `Start` 是任务的开始时间。
- `DueDate` 是任务的截止日期。
- `Importance` 是任务的重要性。将其设置为 `olImportanceHigh`、`olImportanceNormal` 或 `olImportanceLow`。
- `Status` 是任务的状态：`olTaskNotStarted`、`olTaskWaiting`、`olTaskDeferred`、`olTaskInProgress` 或 `olTaskComplete`。
- `PercentComplete` 是任务完成的百分比。
- `Companies` 指定与任务相关的公司。
- `BillingInformation` 是为该任务计单的公司或部门。

以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项。然后设置了任务的状态和正文，指定了一个未来的日期，将状态设置为 `olTaskInProgress`并将完成百分比设置为 10，指定了涉及人员和账单对象，将重要性设置为高，并保存了任务：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTask)

With myTask

  .Subject = "Create a business plan"

  .Body = "The business plan must cover the next four years." & _vbCr & vbCr & "It will provide a detailed budget, staffing projections, and a cost/benefit analysis."

  .DueDate = Str(Date + 28)

  .Status = olTaskInProgress

  .PercentComplete = 10

  .Companies = "Home Polyglot Industrialists"

  .BillingInformation = "Sales & Marketing"

  .Importance = olImportanceHigh

  .Save

End With
```

`TaskItem` 对象总共有 71 个属性。如果您想探索更多属性，请查看此 MSDN 页面：

`http://msdn.microsoft.com/en-us/library/office/jj90814.aspx`

## 允许用户手动分配类别

程序化为项目分配类别可能是困难的，特别是因为许多用户会以独特的方式创建自定义类别或分配类别。在许多情况下，通过在过程的适当时点显示类别对话框，让每个用户手动分配他们偏好的类别会更好。对于由对象变量 `myAppointment` 引用的项目，可以使用该项目的 `ShowCategoriesDialog` 方法。

## 处理任务和任务请求

VBA 可以自动化任务和任务请求。以下章节将向您展示如何创建任务、处理任务内容以及发送任务请求。

### 创建任务

创建一个新的任务项目项，请使用 `Application` 对象的 `CreateItem` 方法并在 `ItemType` 参数中指定 `olTaskItem`。以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTask)
```

### 处理任务项目的内容

要处理任务项目的内容，请设置或获取相应的属性。这些是常用的属性：

- `Subject` 是任务的主题。
- `Body` 是任务的正文内容。
- `Start` 是任务的开始时间。
- `DueDate` 是任务的截止日期。
- `Importance` 是任务的重要性。将其设置为 `olImportanceHigh`、`olImportanceNormal` 或 `olImportanceLow`。
- `Status` 是任务的状态：`olTaskNotStarted`、`olTaskWaiting`、`olTaskDeferred`、`olTaskInProgress` 或 `olTaskComplete`。
- `PercentComplete` 是任务完成的百分比。
- `Companies` 指定与任务相关的公司。
- `BillingInformation` 是为该任务计单的公司或部门。

以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项。它设置了任务的状态和正文，指定了一个未来的日期，将状态设置为 `olTaskInProgress`并将完成百分比设置为10，指定了涉及人员和账单对象，将重要性设置为高，并保存了任务：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTask)

With myTask

  .Subject = "Create a business plan"

  .Body = "The business plan must cover the next four years." &

   "It will provide a detailed budget, staffing projections, and a cost/benefit analysis."

  .DueDate = Str(Date + 28)

  .Status = olTaskInProgress

  .PercentComplete = 10

  .Companies = "Home Polyglot Industrialists"

  .BillingInformation = "Sales & Marketing"

  .Importance = olImportanceHigh

  .Save

End With
```

`TaskItem` 对象总共有 71 个属性。如果您想探索更多属性，请查看此 MSDN 页面：

`http://msdn.microsoft.com/en-us/library/office/jj90814.aspx`

## 允许用户手动分配类别

程序化为项目分配类别可能是困难的，特别是因为许多用户会以独特的方式创建自定义类别或分配类别。在许多情况下，通过在过程的适当时点显示类别对话框，让每个用户手动分配他们偏好的类别会更好。对于由对象变量 `myAppointment` 引用的项目，可以使用该项目的 `ShowCategoriesDialog` 方法。

## 处理任务和任务请求

VBA 可以自动化任务和任务请求。以下章节将向您展示如何创建任务、处理任务内容以及发送任务请求。

### 创建任务

创建一个新的任务项目项，请使用 `Application` 对象的 `CreateItem` 方法并在 `ItemType` 参数中指定 `olTaskItem`。以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTaskItem)
```

### 处理任务项目的内容

要处理任务项目的内容，请设置或获取相应的属性。这些是常用的属性：

- `Subject` 是任务的主题。
- `Body` 是任务的正文内容。
- `Start` 是任务的开始时间。
- `DueDate` 是任务的截止日期。
- `Importance` 是任务的重要性。将其设置为 `olImportanceHigh`、`olImportanceNormal` 或 `olImportanceLow`。
- `Status` 是任务的状态：`olTaskNotStarted`、`olTaskWaiting`、`olTaskDeferred`、`olTaskInProgress` 或 `olTaskComplete`。
- `PercentComplete` 是任务完成的百分比。
- `Companies` 指定与任务相关的公司。
- `BillingInformation` 是为该任务计单的公司或部门。

以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项。它设置了任务的状态和正文，指定了一个未来的日期，将状态设置为 `olTaskInProgress`并将完成百分比设置为10，指定了涉及人员和账单对象，将重要性设置为高，并保存了任务：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTask)

With myTask

  .Subject = "Create a business plan"

  .Body = "The business plan must cover the next four years." &

  vbCr & "It will provide a detailed budget, staffing projections, and a cost/benefit analysis."

  .DueDate = Str(Date + 28)

  .Status = olTaskInProgress

  .PercentComplete = 10

  .Companies = "Home Polyglot Industrialists"

  .BillingInformation = "Sales & Marketing"

  .Importance = olImportanceHigh

  .Save

End With
```

（注：以下示例创建一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项。它设置了任务的状态和正文，）

未来的日期，

任务任务任务：

```
Dim myTask As TaskItem

Set mySearch = Application.CreateItem(ItemType:=TaskTask)
```

## 任务项目的内容

要处理任务项目的内容，请设置或获取相应的属性。这些是最常用的属性：

- `Subject` 是任务的主题。
- `Body` 是任务的正文内容。
- `Start` 是任务的开始时间。
- `DueDate` 是任务的截止日期。
- `Importance` 是任务的重要性。将其设置为 `olImportanceHigh`、`olImportanceNormal` 或 `olImportanceLow`。
- `Status` 是任务的状态：`olTaskNotStarted`、`olTaskWaiting`、`olTaskDeferred`、`olTaskInProgress` 或 `olTaskComplete`。
- `PercentComplete` 是任务完成的百分比。
- `Companies` 指定与任务相关的公司。
- `BillingInformation` 是为该任务计单的公司或部门。

以下示例创建一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项。它设置了任务的状态和正文，指定了一个未来的日期，将状态设置为 `olTaskInProgress`并将完成百分比设置为10，指定了涉及人员和账单对象，将重要性设置为高，并保存了任务：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTask)

With myTask

  .Subject = "Create a business plan"

  .Body = "The business plan must cover the next four years." &

  vbCr & "It will provide a detailed budget, staffing projections, and a cost/benefit analysis."

  .DueDate = Str(Date + 28)

  .Status = olTaskInProgress

  .PercentComplete = 10

  .Companies = "Home Polyglot Industrialists"

  .BillingInformation = "Sales & Marketing"

  .Importance = olImportanceHigh

  .Save

End With
```

`TaskItem` 对象总共有 71 个属性。如果您想探索更多属性，请查看此 MSDN 页面：

`http://msdn.microsoft.com/en-us/library/office/jj90814.aspx`

## 允许用户手动分配类别

程序化为项目分配类别可能是困难的，特别是因为许多用户会以独特的方式创建自定义类别或分配类别。在许多情况下，通过在过程的适当时点显示类别对话框，让每个用户手动分配他们偏好的类别会更好。对于由对象变量 `myAppointment` 引用的项目，可以使用该项目的 `ShowCategoriesDialog` 方法。

## 处理任务和任务请求

VBA 可以自动化任务和任务请求。以下章节将向您展示如何创建任务、处理任务内容以及发送任务请求。

### 创建任务

创建一个新的任务项目项，请使用 `Application` 对象的 `CreateItem` 方法并在 `ItemType` 参数中指定 `olTaskItem`。以下示例创建了一个名为 `myTask` 的 `TaskItem` 对象并将其赋值一个新的任务项目项：

```
Dim myTask As TaskItem

Set myTask = Application.CreateItem(ItemType:=olTaskItem)
```
