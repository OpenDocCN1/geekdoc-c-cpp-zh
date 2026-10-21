+   - A property can be static member, whereas an indexer is always an instance member.
+   - A get accessor of a property corresponds to a method with no parameters, whereas a get accessor of an indexer corresponds to a method with the same formal parameter list as the indexer.
+   - A set accessor of a property corresponds to a method with a single parameter named value, whereas a set accessor of an indexer corresponds to a method with the same formal parameter list as the indexer, plus the parameter named value.
+   - It is an error for an indexer to declare a local variable with the same name as an indexer parameter.

Program 12.8 uses indexers and makes an array of 15 values, stores a few values in the array and the null values of array, from 12th position are stored with the word ‘empty’.

# Program 12.8 | INDEXERS ILLUSTRATED FURTHER

```
using System;
using System.Collections.Generic;
using System.Text;
namespace IndexersExample
{
    class IndexersEx
    {
        private string[] TechCompanies = new string[14];
        public string this[int indexVal]
        {
            get
            {
                if(indexVal <0 || indexVal >= 11)
                    return "empty";
                else
                    return TechCompanies[indexVal];
            }
            set
            {
                if(!(indexVal <0 || indexVal >= 11))
                    TechCompanies[indexVal] = value;
            }
        }
    }
    class theMainClass
    {
        public static void Main()
        {
            IndexersEx Obj = new IndexersEx();
            Obj[0] = "Infosys";
            Obj[3] = "Wipro Infotech";
            Obj[5] = "Sat yam Computers";
            Obj[6] = "Patni Computers";
            Obj[8] = "Hexaware";
            Obj[10] = "Polaris Software";
            Obj[12] = "Mastek Computers";
```