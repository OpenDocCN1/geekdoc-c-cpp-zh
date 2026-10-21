```
using System;
using System.Collections.Generic;
using System.Text;
namespace CaseStudy12
{
    public class AppleComputer
    {
        private string applevariety = "";
        public AppleComputer(string appleComputerVariety)
        {
            this.applevariety = appleComputerVariety;
        }
        public void showAppleComputers()
        {
            System.Console.WriteLine(applevariety);
        }
    }
    public class HPComputer
    {
        private string hpvariety = "";
        public HPComputer(string hpComputerVariety)
        {
            this.hpvaryety = hpComputerVariety;
        }
        public void showHPComputers()
        {
            System.Console.WriteLine(hpvaryety);
        }
    }
    public class AcerComputer
    {
        private string acervariety = "";
        public AcerComputer(string acerComputerVariety)
        {
            this.acervariety = acerComputerVariety;
        }
        public void showAcerComputers()
        {
            System.Console.WriteLine(acervariety);
        }
    }
    class DisplayComputers
    {
        static void Main()
        {
            Console.WriteLine("This is an example of Classes and objects and how they can be used in real world scenarios.");
            AppleComputer mac = new AppleComputer("Apple Power Mac G5");
            AppleComputer gra = new AppleComputer("Apple iMac 2 G4");
            Console.WriteLine("----------------");
            Console.WriteLine("Apple Computer varieties are :");
```