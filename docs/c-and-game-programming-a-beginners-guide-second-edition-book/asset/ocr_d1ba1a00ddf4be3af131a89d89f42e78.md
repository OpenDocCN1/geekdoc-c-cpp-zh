```
class Class1 {
    static void Main() {
        string input;
        int iNumberOne = 0, iNumberTwo = 0; // Local variables

        iNumberTwo = RandomNumber();

        while (iNumberOne != 99) { // 99 ends loop
            Console.Write ("\n Guess the number, hint: "
                + "it's between ten and three.\n"
                + "Can you guess it he, he, he? ");
            input = Console.ReadLine();
            iNumberOne = int.Parse(input);

            if (iNumberOne == iNumberTwo) {
                Console.WriteLine("\n Hey you win, with a smile "
                    + "with a grin!!!");
                iNumberTwo = RandomNumber();
            } else if (iNumberOne > iNumberTwo) {
                Console.WriteLine("\n Too high smart guy!");
                iNumberTwo++;
            } else {
                Console.WriteLine("\n Too low slow Joe");
                iNumberTwo--;
            }
        }

        static int RandomNumber() {
            Random rnd = new Random();
            int n2 = (int)Math.Round(rnd.NextDouble() * 9) + 1;
            return (n2);
        }
    }
}
```

Our next comparison opens the field a bit by making our random function capable of returning character data. Here we also included a while loop that protects our function from returning anything other than a letter (see Example 2.37).