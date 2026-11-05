```
```csharp
        else
            if (speed > 20)
                fine += 100;
        }
    }
}

/* TicketApp.cs        Author:      Doyle
 * Instantiates a Ticket object
 * from the inputted values of
 * speed and speed limit. Uses
 * the year in school classification
 * to set the fine amount.
 * ***********************************/
using System;
namespace TicketSpace
{
    public class TicketApp
    {
        static void Main( )
        {
            int speedLimit,
                speed;
            char classif;

            speedLimit = InputSpeed("Speed Limit", out speedLimit);
            speed = InputSpeed("Ticketed Speed", out speed);
            classif = InputYearInSchool( );

            Ticket myTicket = new Ticket(speedLimit, speed);

            myTicket.SetFine(classif);
            Console.WriteLine("Fine: {0:C}", myTicket.Fine);
            Console.ReadLine();
        }

        public static int InputSpeed(string whichSpeed, out int s)
        {
            string inValue;
            Console.Write("Enter the {0}: ", whichSpeed);
            inValue = Console.ReadLine();
            s = Convert.ToInt32(inValue);
            return s;
        }
    }
}
```
```