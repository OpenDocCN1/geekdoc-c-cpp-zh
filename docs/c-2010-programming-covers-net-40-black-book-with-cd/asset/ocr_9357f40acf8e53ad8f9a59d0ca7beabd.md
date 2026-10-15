```
MGColA.SetItems(1, new Arithmetic(2000));
MGColA.SetItems(2, new Arithmetic(3000));
MGColA.SetItems(3, new Arithmetic(4000));
MGColA.SetItems(4, new Arithmetic(5000));
for (int i = 0; i <= 4; i++)
{
    listBox1.Items.Add(MGColA.GetItems(i));
}
}
public string Sum<T>(T val1, T val2) where T : IBase
{
    return val1.AddIt(val2);
}

public void Display<T>(T val1)
{
    MessageBox.Show(val1.ToString());
}
}
public interface IBase
{
    string AddIt(IBase obj1);
}
public class MyGenericCollection<Tp>
{
    private Tp[] Arr;
    public MyGenericCollection(int size)
    {
        Arr = new Tp[size + 1];
    }
    public Tp GetItems(int index)
    {
        return Arr[index];
    }
    public void SetItems(int index, Tp value)
    {
        Arr[index] = value;
    }
    public int ContainsValue(Tp obj)
    {
        for (int i = 0; i < Arr.Length; i++)
        {
            if (((IEquatable<IBase>)Arr[i]).Equals(obj))
            {
                return i;
            }
        }
        return -1;
    }
}
public class Arithmetic : IEquatable<IBase>, IBase
{
    private int nm;
    public Arithmetic()
    {
        nm = 0;
    }
    public Arithmetic(int Number)
```