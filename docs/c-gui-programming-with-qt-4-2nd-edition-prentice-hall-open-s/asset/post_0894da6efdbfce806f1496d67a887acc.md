
For deleting, we begin by noting the current row. Then we delete the row and submit the change. We must manually submit deletions since the automatic submitter's current index is the row following the deleted row—or the last row if it was the last row that was deleted.

The QDataMapper class makes it easy to develop data-aware forms that display information from a data model. In the example, we used QSqlTableModel as the underlying data model, but QDataMapper can be used with any data model, including non-SQL models. An alternative would have been to use QSqlQuery directly to fill in the form with data and to update the database. This approach requires more work, but it is also more flexible.

In the next section, we will review the rest of the Staff Manager application, including the code that uses the EmployeeForm class developed in this section.

## Presenting Data in Tabular Forms

In many cases, it is simplest to present users with a tabular view of a data set. In this section, we will present the Staff Manager application's main view, which consists of two QTableView in a master-detail relationship. (The form is shown in Figure 13.4.) The master view is a list of departments. The detail view is a list of employees in the current department. Both views use SqlRelationalTableModel, since both of the database tables they are presenting have foreign keys. The relevant CREATE TABLE statements are shown on page 324.

### Figure 13.4. The Staff Manager application

![](img/5a524abdf0b0d58fa99d30abb4463611_528_0.png)

As usual, we use an enum to give meaningful names to the column indexes:

```cpp
enum {
  Department_Id = 0,
  Department_Name = 1,
  Department_LocationId = 2
};
```

We will begin by looking at the MainForm class definition in the header file:

```cpp
class MainForm : public QWidget
{
  Q_OBJECT

public:
    MainForm();

private slots:
    void updateEmployeeView();
    void addDepartment();
    void deleteDepartment();
    void editEmployees();

private:
    void createDepartmentPanel();
    void createEmployeePanel();
};

QSqlRelationalTableModel departmentModel;
QSqlRelationalTableModel employeeModel;

QWidget departmentPanel;
QDialogButtonBox buttonBox;
```

To set up a master-detail relationship, we must make sure that when the user navigates to a new record (row), we update the detail table to show only the relevant records. This is achieved by the private updateEmployeeView() slot. The other three slots do what their names indicate, and the two private functions are helpers for the constructor.

Most of the constructor's code is concerned with the user interface, and setting up suitable signal-slot connections. We will focus on those parts that are relevant to database programming.

```cpp
MainForm::MainForm()
{
    createDepartmentPanel();
    createEmployeePanel();
```

The constructor begins by calling two helper functions. The first creates and sets up the department model and view, and the second does the same for the employee model and view. We will look at the relevant parts of these functions after we have finished looking at the constructor.

The next part of the constructor sets up a layout that contains the two table views, and also sets up the form's buttons. We will skip all this.

```cpp
connect(addButton, SIGNAL(clicked())), this, SLOT(addDepartment()));
connect(deleteButton, SIGNAL(clicked())), this, SLOT(deleteDepartment()));
connect(editButton, SIGNAL(clicked())), this, SLOT(editEmployees()));
connect(quitButton, SIGNAL(clicked())), this, SLOT(close()));

departView->setCurrentIndex(departmentModel->index(0, 0));
```

We connect the buttons to slots in the dialog, and we make sure that the first department is the current item.

Now that we have seen the constructor, we will look at the code in the createDepartmentPanel() helper function that sets up the department model and view:

Code View:

```cpp
void MainForm::createDepartmentPanel()
{
	departmentView = new QWidget();

	departmentModel = new SqlRelationalTableModel(this);
	departmentModel->setTable("department");
	departmentModel->setRelation(Department_LocationId,
		SqlRelation("location", "id", "name"));
	departmentModel->setSort(Department_Name, Qt::AscendingOrder);
	departmentModel->setHeaderData(Department_Name, Qt::Horizontal,
		tr("Dept."));
	departmentModel->setHeaderData(Department_LocationId,
		Qt::Horizontal, tr("Location"));
	departmentModel->select();

	departView = new QTableView;
	departView->setModel(departmentModel);
	departView->setItemDelegate(new SqlRelationalDelegate(this));
	departView->setSelectionMode(QAbstractItemView::SingleSelection);
	departView->setSelectionColumnHidden(QAbstractItemView::SelectRows, 0, true);
	departView->resizeColumnsToContents();
	departView->horizontalHeader()->setStretchLastSection(true);

	departmentLabel = new QLabel(tr("Departments"));
	departmentLabel->setBuddy(departmentView);

	connect(departmentView->selectionModel(),
                SIGNAL(currentRowChanged(const QModelIndex &)),
                this, SLOT(updateEmployeeView()));
}
```

The code begins in a similar way to what we saw in the previous section when we set up a model for the employee. The employee view is a standard QTableView, but because we have a foreign key, we must use SqlRelationalDelegate instead of the raw ID.

The view's selection mode is set to QAbstractItemView::SingleSelection, and its behavior set to QAbstractItemView::SelectRows. This mode means that entire rows are highlighted. We connect the currentRowChanged() signal from the view to the updateEmployeeView() slot.

The inside createEmployeePanel() helper function is similar, but with some important differences:

Code View:

```cpp
void MainForm::createEmployeePanel()
{
	employeePanel = new QWidget();

	employeeModel = new SqlRelationalTableModel(this);
	employeeModel->setTable("employee");
	employeeModel->setRelation(Employee_DepartmentId,
		SqlRelation("department", "id", "name"));
	employeeModel->setSort(Employee_Name, Qt::AscendingOrder);
	employeeModel->setHeaderData(Employee_Name, Qt::Horizontal,
		tr("name"));
	employeeModel->setHeaderData(Employee_Extension, Qt::Horizontal,
		tr("Ext"));
	employeeModel->setHeaderData(Employee_Email, Qt::Horizontal,
		tr("Email"));

	employeeView = new QTableView;
	employeeView->setModel(employeeModel);
	employeeView->setItemDelegate(new SqlRelationalDelegate(this));
	employeeView->setSelectionMode(QAbstractItemView::SingleSelection);
	employeeView->setSelectionBehavior(QAbstractItemView::SelectRows);
	employeeView->setEditTriggers(QAbstractItemView::NoEditTriggers);
	employeeView->horizontalHeader()->setStretchLastSection(true);
	employeeView->setColumnHidden(Employee_Id, true);
	employeeView->setColumnHidden(Employee_DepartmentId, true);
	employeeView->setColumnHidden(Employee_StartDate, true);

	employeeLabel = new QLabel(tr("Employees"));
	employeeLabel->setBuddy(employeeView);
}
```

The employee view's edit triggers are set to QAbstractItemView::NoEditTriggers, effectively making the view read-only. In this application, the user can add, edit, and delete employee records by clicking Edit Employees, which invokes the EmployeeForm in the previous section.

This time, we hide three columns, not just one. We hide the id column, because again that is not meaningful to the user. We also hide the departmentid column because the only employees shown at any one time are those that are in the currently selected department. Finally, we hide the startdate column because it is rarely relevant and can be accessed by clicking Edit Employees.

```cpp
void MainForm::updateEmployeeView() {
	QIndex index = departmentView->currentIndex();
	if (index.isValid()) {
		SqlRecord record = departmentModel->record(index.row());
		int id = record.value("id").toInt();
		employeeModel->setFilter(QString("department = %1").arg(id));
		employeeLabel->setText(tr("E&employees in the %1 Department").arg(record.value("name").toString()));
	} else {
		employeeModel->setFilter("department = -1");
		employeeLabel->setText(tr("E&employees"));
	}
}
```
