![](bbox=[0.125, 0.065, 0.875, 0.405])

# # Looping

```
$process = @(\winword.exe","explorer.exe","vlc.exe","powershell_ise.exe"
foreach ($proc in $process) {
    $data = Get-Object Win32_Process | Where {$_.Name -like $proc}
    $data | Select-Object ProcessId,ExecutablePath,CommandLine | format-wrap
}
```

There are a number of looping structures we can use in PowerShell and we will look a couple of the more common and useful possibilities here. Looping in PowerShell follows the same format as looping in most programming languages. One of the simplest looping constructs we can look at is the for loop: for ($counter=0; $counter -lt 10; $counter++)

```
$ping = New-Object System.Net.NetworkInformation.Ping
$ping.Send($args[0])
Start-Sleep -Second 5
```

We would want to run this script with .looping.ps1 scan.map.org. Let's have a look at what we did here. Here we set up the beginning of our loop for, for $counter=0; counter -lt 10; $counter++. So, this line initializes $counter with zero. The variable keeps track of how many times our for loop has executed. Next, we evaluate $counter to make sure it is still less than 10 with -lt. If this is true, we will continue; if not, we will stop