```
Title ="Professional C# 5.0 and .NET 4.5.1",
Publisher ="Wrox Press",
Isbn ="978-1-118-83303-2"
});
}

public Book GetTheBook() => books[0];
}
}
```

The ObjectDataProvider element can be defined in the resources section. The XML attribute ObjectType defines the name of the class; with MethodName you specify the name of the method that is invoked to get the book object (code file BooksDemoLib/Controls/BookUC.xaml):

```
<DockPanel.Resources>
<ObjectDataProvider x:Key="theBook"
ObjectType="local:BooksRepository"
MethodName="GetTheBook" />
</DockPanel.Resources>
```

The properties you can specify with the ObjectDataProvider class are listed in the following table:

| ObjectDataProvider Property | Description |
|---|---|
| ObjectType | Defines the type to create an instance. |
| ConstructorParameters | Using the ConstructorParameters collection, you can add parameters to the class to create an instance. |
| MethodName | Defines the name of the method that is invoked by the object data provider. |
| MethodParameters | Using this property, you can assign parameters to the method defined with the MethodName property. |
| ObjectInstance | Using this property, you can get and set the object that is used by the ObjectDataProvider class. For example, you can assign an existing object programmatically rather than define the ObjectType so that an object is instantiated by ObjectDataProvider. |
| Data | Enables you to access the underlying object that is used for data binding. If the MethodName is defined, with the Data property you can access the object that is returned from the method defined. |

# List Binding

Binding to a list is more frequently done than binding to simple objects. Binding to a list is very similar to binding to a simple object. You can assign the complete list to the DataContext from code-behind, or you