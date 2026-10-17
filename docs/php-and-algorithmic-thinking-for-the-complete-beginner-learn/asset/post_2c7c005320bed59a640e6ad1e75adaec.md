

## Exercise 31.4-5 Is the Number a Prime?

```php
<?php
echo "Enter an integer greater than 1: ";
$x = trim(fgets(STDIN));

$number_of_divisors = 2;
for ($i = 2; $i <= intval($x / 2); $i++) {
    if ($x % $i == 0) {
        $number_of_divisors++;
        break;
    }
}

if ($number_of_divisors == 2) {
    echo "Number ", $x, " is prime";
}
?>
```

## Second Approach – Using a pre-test loop structure

You can convert the counted loop structure to a pre-test loop structure and then change the Boolean expression of the loop to evaluate both variables $i$ and $number_of_divisors$. As long as variable $number_of_divisors$ is equal to 2, the loop should continue iterating. The PHP script is as follows.

```php
<?php
echo "Enter an integer greater than 1: ";
$x = trim(fgets(STDIN));

$number_of_divisors = 2;
$i = 2;
while ($i <= intval($x / 2) && $number_of_divisors == 2) {
    if ($x % $i == 0) {
        $number_of_divisors++;
    }
    $i++;
}

if ($number_of_divisors == 2) {
    echo "Number ", $x, " is prime";
}
?>
```

## Exercise 31.4-6 Finding all Prime Numbers from 1 to N

Write a PHP script that prompts the user to enter a positive integer and then displays all prime numbers from 2 to that given integer. Moreover, the script should validate data input and display an error message when the user enters any values less than 2.

# Solution

To help you, this exercise is solved using the “from inner to outer” method.

The inner code fragment that checks whether variable $x contains a prime number has already been discussed in the previous exercise, so you can use it as is. On the other hand, the outer PHP script follows and is shown in general form.

```php
echo "Enter an integer greater than 1: ";
$N = trim(fgets(STDIN));
while ($N < 2) {
    echo "Wrong number. Please enter an integer greater than 1: ";
    $N = trim(fgets(STDIN));
}

for ($x = 1; $x <= $N; $x++) {
    //Here goes the code that checks whether variable $x
    //contains a prime number
}
```

Thus, combining both scripts, the final PHP script becomes

```php
<?php
echo "Enter an integer greater than 1: ";
$N = trim(fgets(STDIN));
while ($N < 2) {
    echo "Wrong number. Please enter an integer greater than 1: ";
    $N = trim(fgets(STDIN));
}

for ($x = 1; $x <= $N; $x++) {
    $number_of_divisors = 2;
    $i = 2;
    while ($i <= intval($x / 2) && $number_of_divisors == 2) {
        if ($x % $i == 0) {
            $number_of_divisors++;
        }
        $i++;
    }
    if ($number_of_divisors == 2) {
        echo "Number ", $x, " is prime\n";
    }
}
?>
```

## Exercise 31.4-7 Heron’s Square Root

Write a PHP script that prompts the user to enter a non-negative value and then calculates its square root using Heron’s formula, as follows.

\(x_{n+1} = \frac{\left(x_n + \frac{y}{x_n}\right)}{2}\)

where

- y is the number for which you want to find the square root
- xn is the n-th iteration value of the square root of y

Moreover, the script should validate data input and display an error message when the user enters any non-numeric or negative values.

# Solution

It is almost certain that you are a little bit confused and you are scratching your head right now. Don’t be scared by all this math stuff! You can try to understand Heron’s formula through the following flowchart instead!

![](img/4d9a992abc5da7946ac44f9e6bf1d032_545_0.png)

Still confused? Let’s see an example. Let’s find the square root of 25:

- Assume 8 as your first guess.
- The product of 8 × 8 is 64.
- Since 64 isn’t “close enough” to 25, you can create a new guess by calculating the expression

\(\frac{\left(guess + \frac{number}{guess}\right)}{2} = \frac{\left(8 + \frac{25}{8}\right)}{2} \approx 5.56\)

- The product of 5.56 × 5.56 is about 30.91
- Since 30.91 isn’t “close enough” to 25 you can create a new guess by calculating the expression

\[
\frac{guess + \frac{number}{guess}}{2} = \frac{5.56 + \frac{25}{5.56}}{2} \approx 5.02
\]

- The product of 5.02 × 5.02 is 25.2
- You can say that 25.2 is actually “close enough” to 25. Therefore, you can stop the whole process and say that the approximate square root of 25 is 5.02

Now, let’s see the corresponding PHP script.

```php
<?php
define("ACCURACY", 0.000000000001);

echo "Enter a non-negative number: ";
$y = trim(fgets(STDIN));
while (is_numeric($y) != true || $y < 0) {
    echo "Invalid value. Enter a non-negative number: ";
    $y = trim(fgets(STDIN));
}
$guess = rand(1, $y);    //Make a random first guess
                         //between 1 and given value

while (abs($guess * $guess - $y) > ACCURACY) {  //Is it "close enough"?
    $guess = ($guess + $y / $guess) / 2;        //No, create a new "guess"!
}

echo $guess;
?>
```

> **Notice:** Please note the way that “Is it close enough” is checked. When the absolute value of the difference \(|guess^2 - given\_value|\) becomes less than 0.000000000001, the flow of execution exits the loop.

## Exercise 31.4-8 Calculating π

Write a PHP script that calculates π using the Madhava–Leibniz<sup>2,3</sup> series, which follows, with an accuracy of 0.00001.

\(\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots\)

# Solution

The Madhava–Leibniz series can be solved for π, and becomes

\(\pi = \frac{4}{1} - \frac{4}{3} + \frac{4}{5} - \frac{4}{7} + \cdots\)

The more fractions you have, the better the accuracy! Thus, to calculate this formula the script needs to perform many iterations so as to use as many fractions as possible. But, of course, it can’t iterate forever! The loop should actually stop iterating when the current value of π and the one calculated in the previous iteration are “close enough,” which means that the absolute value of their difference has become very small. The constant `ACCURACY` defines how small this difference should be. The PHP script is shown here.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_547_0.png)

<sup>2</sup> Madhava of Sangamagrama (c. 1340–c. 1425), was an Indian mathematician and astronomer from the town of Sangamagrama (present day Irinjalakuda) of India. He founded the Kerala School of Astronomy and Mathematics and was the first to use infinite series approximations for various trigonometric functions. He is often referred to as the “father of mathematical analysis.”

<sup>3</sup> Gottfried Wilhelm von Leibniz (1646–1716) was a German mathematician and philosopher. He made important contributions to the fields of metaphysics, logic, and philosophy, as well as mathematics, physics, and to history. In one of his works, _On the Art of Combination (Dissertatio de Arte Combinatoria)_, published in 1666, he formulated a model that is considered the theoretical ancestor of modern computers.

```php
echo "Pi ~ ", $pi;
?>
```

> Notice: Please note the way in which variable $sign toggles between the values -1 and +1 in each iteration.

If you reduce the value of the constant ACCURACY, π will be calculated more and more accurately. Depending on how fast your computer is, you can calculate the first six digits of π fairly quickly. However, the time it takes to calculate each succeeding digit of π goes up exponentially. To calculate 30 digits of π on a modern computer using this method could take years!

## Exercise 31.4-9 Approximating a Real with a Fraction

Write a PHP script that prompts the user to enter a real between 1 and 100 and then tries to find the fraction N/M that better approximates it, where N is an integer between 0 and 100 and M is an integer between 1 and 100. Moreover, the script should validate data input, allowing the user to enter only numeric values between 0 and 100. There is no need to display any error messages.

# Solution

The solution is simple. All you need to do is iterate through all possible combinations of variables $n and $m and check which one better approximates the real given.

To iterate through all possible combinations of variables $n and $m, you can use a nested loop control structure, that is, two counted loop structures, one nested within the other, as follows.

```php
for ($n = 0; $n <= 100; $n++) {
    for ($m = 1; $m <= 100; $m++) {
        ...
    }
}
```

> Notice: The total number of iterations is 101 × 100 = 10100. Quite a big number but, for a modern computer, this is peanuts!

The following criteria

minimum of (|N/M − real given|)

can evaluate how “good” an approximation is.

Confused? Let’s try to approximate the value 0.333 with a fraction, iterating through all possible combinations of N and M.

- ➤ For N = 1, M = 1 the criteria equals to |1/1 − 0.333| = 0.6670

