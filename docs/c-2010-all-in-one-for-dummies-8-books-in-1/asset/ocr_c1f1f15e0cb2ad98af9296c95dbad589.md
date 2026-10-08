# 778 Running with the Dynamic Runtime

```
def main
  Array.new(11) { gets.to_i }.reverse.do |x|
    y = f(x)
    puts "#{x} #{(y>400) ? 'TOO LARGE' : y"
  end
end
```

This isn't a Ruby book, and that fact it isn't lost on me. Nonetheless, this is the best dynamic language that I can use for an example — bar bone.

Two functions are: f and main. Main accepts 11 numbers from the console and moves them to an integer array (that's what gets.to_i does). For each value in the array, it sets y equal to f(x) and then sees if it is higher than our arbitrary value. If it prints "TOO LARGE"; otherwise, it prints the numbers.

Why is dynamic important for this algorithm? It isn't. Could you not all statically typed? The dynamic bit has an impact, though.

First, f(x) doesn't care what x is. The program assumes that whatever comes in gets changed to an integer at gets.to_i, but the function itself is agnostic. This is good and bad, because if we happen to give it a string or some other type, it will fail.

The array itself isn't typed, either. This can have benefits, because it is possible to drop a differently typed value there if you know you are just going to write to the screen.

# Dynamic C#

Of course, C# now has similar features, right? We should be able to do the same thing! Yes, in fact, Here's the code:

```
static dynamic f(dynamic x)
{
  return (Math.Sqrt(x) + 5.0 * Math.Pow(x, 3.0));
}
static void Main(string[] args)
{
  dynamic[] array = new Array[il];
  for (int i = 0; i < 11; i++)
    array[i] = Console.ReadLine();
  }
  for (int i = 10; i>=0; i--)
{
```