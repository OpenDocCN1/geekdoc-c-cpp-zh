```
```csharp
using System.Threading.Tasks;
namespace JoggingDistance
{
    class JoggingDistance
    {
        static void Main(string[] args)
        {
            int initialStrideCount,
                finalStrideCount,
                hrs,
                mins,
                totalMinutes;
            double numberOfStepsPerMin,
                distanceTraveled;

            DisplayInstructions();

            initialStrideCount = GetNumberStrides("first");
            finalStrideCount = GetNumberStrides("last");
            InputJoggingTime(out hrs, out mins);

            totalMinutes = CalculateTime(hrs, mins);
            numberOfStepsPerMin = CalculateAvgSteps
                (initialStrideCount,
                finalStrideCount);
            distanceTraveled = CalculateDistance(numberOfStepsPerMin,
                totalMinutes);
            DisplayResults(numberOfStepsPerMin, hrs, mins,
                distanceTraveled);
            Console.ReadKey();
        }

        public static void DisplayInstructions()
        {
            Console.WriteLine("How many miles did you jog?");
            Console.WriteLine("Distance (in miles) will be " +
                "calculated");
            Console.WriteLine("based on stride and number of steps");
            Console.WriteLine("taken per minute.\n");
            Console.WriteLine("You will be asked to enter ");
            Console.WriteLine("your initial and ending strides...");
            Console.WriteLine("OR how many steps you took the ");
            Console.WriteLine("first minute and how many ");
            Console.WriteLine("steps during the last minute.");
            Console.WriteLine("Average stride is calculated from ");
            Console.WriteLine("those entries.\n");
            Console.WriteLine("Calculations are based on a ");
            Console.WriteLine("2.5 feet stride-each step is 2.5 " +
                "feet long.");
        }
    }
}
```
```