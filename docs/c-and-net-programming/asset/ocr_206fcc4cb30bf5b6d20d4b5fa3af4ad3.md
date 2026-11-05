```
```csharp
namespace ConsoleApplication1
{
    class ProgramSort
    {
        static void Main()
        {
            List<string> names = new List<string>();
            names.Add("Riya");
            names.Add("Bina");
            names.Add("Abha");
            names.Add("Gita");
            names.Add("Tina");
            names.Sort();
            foreach (string s in names)
                Console.WriteLine(s);
            Console.ReadLine();
        }
    }
}
```
```