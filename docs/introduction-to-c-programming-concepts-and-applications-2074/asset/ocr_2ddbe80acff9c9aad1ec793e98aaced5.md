sentinel is a deliberately unusual value that you wouldn't normally encounter, it's a value you use to identify when you're processing "regular" data. A negative balance in a bank account could be a sentinel, assuming you're not allowed to have an overdrawn account. You can use sentinels to help identify when it's time to break out of a loop. If a sentinel value causes, the loop will be skipped over.

There's a good chance that you'll accidentally create an infinite loop at some point in your program. It's a common pitfall that it's easy to make if you're writing a loop condition, so it's better to figure out early on on how to break out of one when it happens.

| // Program 5_5 |
| // Infinite Loop |
| #include <iostream> |
| using namespace std; |
| int main() {
| int count = 1; |
| while (count > 0) {
| cout << count << endl; |
| count++; |
| }

One problem you might be aware of is that when you're figuring out average age, you'll want to divide the sum of the ages by the number of people. If you're performing integer division. Remember that this gives only the quotient between them, ignoring any remainder. To deal with this, you'll need to convert one or both of the numbers to a floating-point value.

If the condition never becomes false, then every time the condition is evaluated, it's true, so the loop repeats forever. This is an infinite loop.

For example, if Program 5_5 keeps printing consecutive numbers, starting at 1; notice that the condition is greater than 0, which is always true. If you run this program, the loop will keep going forever, until you do something special to stop it.

You can do this by casting a value, which is a way of converting a value of one type into another of another type. To do this, you have two options: you can put the new type in parentheses in front of the value you want to cast, or you can state the new type and then put the value to convert. Either way, you'll convert the value, if possible, to the other type.

Generally, the way you stop the program will depend on your system. Your IDE will have a Button of something that will cause it to stop; or others, you can hit Ctrl+C, that will call the program to "break" and stop. In the worst case, you might have to actually stop your entire system by closing window you are running the program in.

| // Program 5_9 |
| Type conversions |
| #include <iostream> |
| using namespace std; |
| int main() {
| int a = 3; |
| float b = 2.6; |
| bool c = true; |
| cout << (float)a << " " << (float)a << endl;
| cout << (bool)a << " " << (bool)a << endl;
| cout << (int)b << " " << (int)b << endl;
| cout << (bool)b << " " << (bool)b << endl;
| cout << (int)c << " " << (int)c << endl;
| cout << (float)c << " " << (float)c << endl;
| }

For the 3 types you've seen so far (integers, floating-point values, and Boolean variables), it's possible to convert one type to either of the others, as Program 5_9 shows. Note that there are some types you can't convert, as strings of text and self-defined types.

If you are prepared to stop the infinite loop, try programming one yourself.