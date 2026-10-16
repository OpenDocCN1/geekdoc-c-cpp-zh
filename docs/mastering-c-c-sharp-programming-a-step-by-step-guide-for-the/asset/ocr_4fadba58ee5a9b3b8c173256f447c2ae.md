```
count--;
}
}
}
Console.WriteLine("HandleFile exit");
return count;
}
}
```

Output:

HandleFile enter

Please be patient while I do something that is important.

HandleFile exit

Count: <number_of_characters>

In this example, we have our Main method and after that, we create a Task instance. We pass in an argument (parameter) of ProcessDataAsync and then, in the following line, we use task.Start() to start the task. We wait for it to end using the task.Wait() method.

ProcessDataAsync is, as you should have guessed, an asynchronous method and that means it is mandatory to use the await keyword. In the method Task<int> task = HandleFileAsync('C:\enable1.txt'), the first code line is calling a method called HandleFileAsync. Because that method is an asynchronous method, the control will return to this method before HandleFileAsync returns.

While HandleFileAsync is doing its job, a message is displayed on the screen that reads “HandleFile enter” and “Please be patient while I do something that is important”. The first line of that message is from the HandleFileAsync method and this happens because the method is printed to the screen when it is called and control is