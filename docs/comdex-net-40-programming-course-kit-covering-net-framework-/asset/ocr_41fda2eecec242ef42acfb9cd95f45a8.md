22. Click the **Preview** button to view the data from the database in the **Results** pane (Fig.C#-4.24).

23. Click the **Close** button to close the **Preview Data** dialog box (Fig.C#-4.24).

In this way you can access data from a database through a data adapter.

# Creating a Dataset

Dataset, as already explained, contains a cached copy of the tables of a database. The dataset is independent of the database; and therefore, the interaction between a dataset and a database is done through a data adapter. You can fill data in a dataset by using the Fill() method of the data adapter.

Perform the following steps in the **DataAdapter** application to create a dataset:

+   1. Click **Data→Generate Dataset** on the menu bar, as shown in Fig.C#-4.25:

![](bbox=[0.294, 0.293, 0.729, 0.541])

Fig.C#-4.25

The **Generate Dataset** dialog box appears, prompting you to select a dataset, as shown in Fig.C#-4.26:

![](bbox=[0.405, 0.583, 0.619, 0.715])

Fig.C#-4.26

You can select an existing dataset or create a new dataset. By default, the **New** radio button is selected. You can provide a desired name to the new dataset or you can use the default name **DataSet1**. The **Generate Dataset** dialog box also prompts you to select a table to be added to the dataset. By default, the **Employees** table is selected (Fig.C#-4.26). This is because we have already added the **Employees** table in the **DataAdapter** application.

+   2. Click the **OK** button to add the dataset to the **DataAdapter** application (Fig.C#-4.26).

The dataset, **dataSet11**, is added to the component tray, as shown in Fig.C#-4.27: