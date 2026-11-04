```
NotifyPropertyChanged("Make");
}
}
public string Model
{
    get { return _model; }
    set
    {
        if (_model != value)
        {
            _model = value;
            NotifyPropertyChanged("Model");
        }
    }
}
```

# 11. Run the application again.

Now when you click the Change Data Context Value with Code-Behind button, the changed values get reflected automatically in the TextBox elements. This is due to the combination of the TwoWay binding mode as well as the implementation of INotifyPropertyChanged. (See Figure 3-3.)

![](bbox=[0.26, 0.6, 0.68, 0.82])

Figure 3-3:
TwoWay Data Binding with INotifyPropertyChanged.

# Validating data

It's good practice to validate any input provided to you from the user. People aren't perfect, and some people can be downright malicious. WPF provides a built-in framework for data validation and error notification. It's available to you through the implementation of the IDataErrorInfo interface on your classes.

You can add validation to the Car class you already created in Binding Sample2 from the preceding section.