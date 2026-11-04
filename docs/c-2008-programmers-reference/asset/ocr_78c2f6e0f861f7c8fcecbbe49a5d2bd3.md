A better way to resolve this issue is to expose BranchName as a property of type Collection<T> instead of List<T>. That’s because the generic Collection<T> type provides four overridable methods — ClearItems(), InsertItem(), RemoveItem(), and SetItem() — which allow a derived class to be notified when a collection has been modified.

Here’s how rewriting the Branch class, using the generic Collection<T> type, looks:

```
~~~csharp
    public class Branch
    {
        public Branch()
        {
            _branchNames = new BranchNamesCollection(this);
        }

        private BranchNamesCollection _branchNames;
        public Collection<string> BranchNames
        {
            get
            {
                return _branchNames;
            }
        }

        //---event raised when an item is removed---
        public event EventHandler ItemRemoved;

        //---called from within the BranchNamesCollection class---
        protected virtual void RaiseItemRemovedEvent(EventArgs e)
        {
            if (ItemRemoved != null)
            {
                ItemRemoved(this, e);
            }
        }

        private class BranchNamesCollection : Collection<string>
        {
            private Branch _b;
            public BranchNamesCollection(Branch b)
            {
                _b = b;
            }

            //---fired when an item is removed---
            protected override void RemoveItem(int index)
            {
                base.RemoveItem(index);
                _b.RaiseItemRemovedEvent(EventArgs.Empty);
            }
        }
    }
~~~
```