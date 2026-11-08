```
```csharp
public int[] arr = new int[10];
public int this[int item]
{
    get
    {
        return arr[item];
    }
    set
    {
        arr[item] = value;
    }
}
public void InitializeArray()
{
    Random rand = new Random();
    int item = rand.Next(100);
    for (int i = 0; i < size; i++)
    {
        this.arr[i] = item;
        item += 1;
    }
}
//Defining Operator overloading method for addition
public static Array operator +(Array arr1, Array arr2)
{
    Array resultArr = new Array();
    for (int i = 0; i < size; i++)
    {
        resultArr[i] = arr1[i] + arr2[i];
    }
    return resultArr;
}
//Defining Operator overloading method for multiplication
public static Array operator *(Array arr1, Array arr2)
{
    Array resultArr = new Array();
    for (int i = 0; i < size; i++)
    {
        resultArr[i] = arr1[i] * arr2[i];
    }
    return resultArr;
}
public void PrintArray()
{
    for (int i = 0; i < this.arr.Length; i++)
    {
        Console.WriteLine(arr[i]);
    }
}
}
```
```

In the preceding code, we have declared an Array class with two methods to add and multiply the array objects using operator overloading. After that, we have first fixed the number of array elements to 10 and then initialized the elements by using the InitializeArray() method. This method first gets a random number whose range is specified to 100, increments the number by one, and then stores it in the array. In the Main() method, we have first initialized the two arrays and then applied the operator overloading method for both addition and multiplication. The output of the program is given as follows: