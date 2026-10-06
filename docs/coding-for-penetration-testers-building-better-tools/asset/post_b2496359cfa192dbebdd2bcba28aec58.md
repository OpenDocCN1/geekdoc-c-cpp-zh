
```
Write-Output "Hello World"
```

That's all there is to it. After saving the file, we can either run it code manually by opening a PowerShell shell, navigating to it, and then running HelloWorld.PS1, or by clicking on the green triangle (10th from the left) in the toolbar of ISE. In ISE, we will see the output from our script execution in the middle window of the interface. Write-Output is one of the PowerShell cmdlets we discussed earlier in this section, and it contains all the necessary functionality to print our statement. Also notice that, unlike our example in bash, we did not need to use anything like a shebang in order to indicate the interpreter we needed to use. In Windows, this function is handled through the use of the file extension .PS1, which indicates that the script should be handled by PowerShell.

## Variables

Variables under PowerShell are, again, very similar to what we might find by bash. By default, variables have no type, meaning that a given variable can contain text or numeric data. Variables are always addressed as $<variable name>, whether assigning data to them or extracting data from them. Let's look at a quick variable example and a new cmdlet:

```bash
$processes = Get-Process powershell_ise
$processes
```

In this case, we are invoking the Get-Process cmdlet to get the process information for the ISE application we are using to develop our scripts. We are taking the returned data from the cmdlet and storing it in the $processes variable. On the next line, we are echoing out the contents of $processes. If everything was successful, when we press run, we should see output similar to Table 1.3.

## Table 1.3

Output from Get-Process powershell_ise

| Handles | NPM (K) | PM (K) | WS (K) | VM (M) | CPU (s) | Id | ProcessName |
|---|---|---|---|---|---|---|---|
| 769 | 73 | 138212 | 185684 | 970 | 8.73 | 2612 | powershell_ise |

The return from the cmdlet we echoed contains the information on the handles, nonpaged memory, paged memory, working set, virtual memory, CPU usage, process ID, and process name of the process on which we requested information. Also notice that the formatted output of the cmdlet survives being stored in a variable and echoed out again.

We can also do local and global variable scoping in PowerShell. With variable scoping we can limit a variable to a portion of code or function. By using functions we can see a nice demonstration of how to deal with variable scope.

```powershell
function hello {
    $LOCAL:name = "whoever you are"
    write-output "hello there $name"
}
$name = $args[0]
write-output "hello there $name"
hello
write-output "hello there $name"
```

The first item we find in our script is the function we use to demonstrate the scope of our variable. Functions in PowerShell are very similar to those we discussed when we went over the same topic in bash. The first line of the function is simply the function tag, the name by which we want to refer to the function, in this case hello, and the opening curly bracket, {, to start the function. On the first line inside the function, we can see the line creating our local variable. This variable, created with the local keyword, will only exist inside the scope of our function, and the function will keep its own copy of the contents, regardless of what we name it. Here, we set the contents of $LOCAL:name to the string whoever you are. On the next line, we echo out a greeting and the contents of the variable, then close up the function with }.

In the main body of the script, we take in an argument from the command line, $args[0], and place the contents of it $name. Notice that this is the same variable name we used in our function, without the LOCAL tag to set the variable scope, this implicitly makes the variable global in scope. Next, we echo out our greeting and variable contents of $name, run the function, and echo the greeting and variable again. We can see from the output in Fig. 1.11, even though we changed the contents of our local copy of $name in the function, we did not change the contents of the same variable in the main body of the script, due to the difference in variable scopes. To run our script with command line arguments...
