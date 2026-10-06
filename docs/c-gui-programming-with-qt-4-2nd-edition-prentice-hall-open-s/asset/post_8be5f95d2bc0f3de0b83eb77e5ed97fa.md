
```cpp
employeeModel->select();
employeeView->horizontalModel->setVisible(
employeeModel->rowCount() > 0);
}
```

Whenever the current department changes (including at startup), this slot is called. If there is a valid current department, the function retrieves the department's ID and sets a filter on the employee model. This constrains the employees to those with a matching department ID foreign key. (A filter is just a WHERE clause without the WHERE keyword.) We also update the label that is shown above the employee to show the name of the department employees are in.

If there is no valid department (e.g., if the database is empty), we set the filter to match a non-existent department ID to ensure no records match.

We then call select() on the model to apply the filter. In turn we will emit signals that the view will respond by updating itself. Finally, we show or hide the employee's column headers depending on whether or not any employees are shown.

```cpp
void MainForm::addDepartment()
{
    int row = departmentModel->rowCount();
    departmentModel->insertRow(row);
    QModelIndex index = departmentModel->index(row, Department_Name);
    departmentView->setCurrentIndex(index);
    departmentView->edit(index);
}
```

If the user clicks the Add Dept. button, we insert a new row at the end of the department table, make this row current, and initiate editing of the department name column as though the user had pressed F2 or double-clicked it. If we needed to provide some default values, we would do so by calling insertRow() call.

We have not to concern ourselves with creating unique keys for new records because we have used an auto-incrementing column to handle this for us. If this approach is not possible or suitable, we connect to the model's beforeInsert() signal. This is emitted after the user's edits, just before the insertion takes place in the database. There are similar beforeDelete() and beforeUpdate()

```cpp
void MainForm::deleteDepartment()
{
    QModelIndex index = departmentView->currentIndex();
    if (!index.isValid()) {
        return;
    }

    QSqlDatabase::database().transaction();
    QSqlRecord record = departmentModel->index(index.row());
    int id = record.value(Department_Id).toInt();
    int numEmployees = 0;

    QSqlQuery query(QString("SELECT COUNT(*) FROM employee "
        "WHERE departmentid = %1").arg(id));
    if (query.next()) {
        numEmployees = query.value(0).toInt();
        if (numEmployees > 0) {
            int r = QMessageBox::warning(this, tr("Delete Department"),
                tr("Delete %1 and all its employees?")
                .arg(record.value(Department_Name).toString()),
                QMessageBox::Yes | QMessageBox::No);
            if (r == QMessageBox::No) {
                QSqlDatabase::database().rollback();
                return;
            }
        }
        query.exec(QString("DELETE FROM employee "
            "WHERE departmentid = %1").arg(id));
    }

    departmentModel->removeRow(index.row());
    departmentModel->removeAll();
    QSqlDatabase::database().commit();
}
```

If the user wants to delete a department, we let them do without formality if the department has no employees. But if it has employees, we ask the user to confirm the deletion, and if they confirm, we do a cascading delete to ensure that the relational integrity is maintained. To achieve this, at least for databases as SQLite 3 which doesn't enforce relational integrity for us, we must use a transaction.

Once the transaction has been initiated, we execute a query to find out how many employees are in the department. If there is at least one, we pop up a message box asking for confirmation. If the user says no, we roll back the transaction and return. Otherwise, we delete all the department's employees as well as the department itself, and we commit the transaction.

```cpp
void MainForm::editEmployees(){
    int employeeId = -1;
    QModelIndex index = employeeView->currentIndex();
    if (index.isValid()){
        QSqlRecord record = employeeModel->record(index.row());
        employeeId = record.value(Employee_Id).toInt();
    }

    EmployeeForm form(employeeId, this);
    form.exec();
    updateEmployeeView();
}
```

The editEmployees() slot is invoked whenever the user clicks the Edit Employees button. We begin by assigning an invalid employee ID. Then we overwrite this with the current employee's ID if possible. Then we construct the EmployeeForm and show it modally. Finally, we call the updateEmployeeView() slot to make the form's detail table view refresh itself since changes to employees may have occurred.

This chapter showed that Qt's view classes make viewing and editing data in SQL databases as easy as possible. In situations where we want to present records using a form view, we can use QDataMapper to map widgets to the user interface to the fields in a record of the database. Setting master-detail relationships is quite easy, requiring just one signal-slot connection and the implementation of one simple slot. Drill-down is also straightforward, just requiring us to navigate to the selected record in the drilled-down form's constructor, or to go to the first record if no record is selected.

# 4. Multithreading

![](img/5a524abdf0b0d58fa99d30abb4463611_536.png)

- Creating Threads
- Synchronizing Threads
- Communicating with Main Thread
- Using Qt Classes in Secondary Threads

Conventional GUI applications have one thread of execution and perform one operation at a time. If the user invokes a time-consuming operation from the user interface, the interface typically freezes. Chapter 7 presents some solutions to this problem. Multithreading is another solution.

In a multithreaded application, the GUI runs in its own thread and additional processing takes place in one or more threads. When running on a single processor, multithreaded applications may run slower than singlethreaded equivalent due to the overhead of having multiple threads. But on multiprocessor systems, which are becoming increasingly common, multithreaded applications can execute several threads simultaneously, resulting in performance.

In this chapter, we will start by showing how to subclass QThread and how to use QMutex, QSemaphore, and QWaitCondition to synchronize threads.* Then we will see how to communicate with the main thread from secondary threads. Finally, we round off with a review of which classes can be used in secondary threads and which cannot.*4.4 is expected to provide a higher-level threading API, supplementing the threading classes described here, to make writing multreaded applications less error-prone.

Multithreading is a large topic with many books devoted to the subject—for example, Threads Primer: A Guide to Multithreaded Programming by Bill Lewis and Daniel J. Berg (Prentice Hall, 1995) and Multithreaded, Parallel, and Distributed Programming by Gregory Andrews (Addison-Wesley, 2000). Here it is assumed that you already understand the fundamentals of multithreaded programming, so the focus is on how to develop multreaded applications rather than the subject of threading.

# Creating Threads

Providing multiple threads in a Qt application is straightforward: We just subclass QThread and reimplement its run() function. To show how this works, we will start by reviewing the code for a very simple QThread subclass that repeatedly prints a string on a console. The application's user interface is shown in Figure 14.1.

```cpp
class Thread : public QThread
{
    Q_OBJECT

public:
    Thread();

    void setMessage(const QString &message);
    void stop();

protected:
    void run();

private:
    QString messageStr;
    volatile bool stopped;
};
```

# Figure 14.1. The Threads application

![](img/5a524abdf0b0d58fa99d30abb4463611_537.png)

The Thread class is derived from QThread and reimplements the run() function. It provides two additional functions: setMessage() and stop().

The stopped variable is declared volatile because it is accessed from different threads and we want to be sure that it is freshly read every time it is needed. If we omitted the volatile keyword, the compiler might optimize access to the variable, possibly leading to incorrect results.

```cpp
Thread::Thread()
{
    stopped = false;
}
```

We set stopped to false in the constructor.
