fetching data from a remote server or performing database queries.

# **Example**: Asynchronous Data Loading in WPF

```
```csharp
using System;
using System.Collections.ObjectModel;
using System.ComponentModel;
using System.Threading.Tasks;
using System.Windows;

namespace WpfApp
{
    public partial class MainWindow : Window,
INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler
PropertyChanged;

        private ObservableCollection<string> dataList;
        public ObservableCollection<string> DataList
        {
            get { return dataList; }
            set
            {
                dataList = value;
                PropertyChanged?.Invoke(this, new
PropertyChangedEventArgs(nameof(DataList)));
            }
        }

        public MainWindow()
        {
            InitializeComponent();
            DataContext = this;

            // Load data asynchronously
```
```