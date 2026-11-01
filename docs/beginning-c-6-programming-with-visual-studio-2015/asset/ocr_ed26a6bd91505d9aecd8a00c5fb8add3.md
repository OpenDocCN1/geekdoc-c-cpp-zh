8. Add a new class called SuperCow and modify the code in SuperCow.cs as follows:

```
public class SuperCow : Cow
{
    public void Fly()
    {
        WriteLine($"{name} is flying!");
    }
    public SuperCow(string newName) : base(newName)
    {
    }
    public override void MakeANoise()
    {
        WriteLine(
            $"{name} says 'here I come to save the day!'" );
    }
}
```

9. Add a new class called Farm and modify the code in Farm.cs as follows:

```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Ch12Ex04
{
    public class Farm<T> : IEnumerable<T>
        where T : Animal
    {
        private List<T> animals = new List<T>();
        public List<T> Animals
        {
            get { return animals; }
        }
        public IEnumerator<T> GetEnumerator() => animals.GetEnumerator();
        IEnumerator IEnumerable.GetEnumerator() => animals.GetEnumerator();
        public void MakeNoises()
        {
            foreach (T animal in animals)
            {
                animal.MakeANoise();
            }
        }
        public void FeedTheAnimals()
        {
            foreach (T animal in animals)
            {
                animal.Feed();
            }
        }
        public Farm<Cow> GetCows()
        {
            Farm<Cow> cowFarm = new Farm<Cow>();
```