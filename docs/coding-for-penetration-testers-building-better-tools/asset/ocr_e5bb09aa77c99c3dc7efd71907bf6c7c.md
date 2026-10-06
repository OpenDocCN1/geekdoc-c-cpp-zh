```
Get-ChildItem
hklm:software/windows/currentversion/uninstall/ |
  ? {$_.ValueCount -gt 0 } |
  ForEach-Object { Write-Host $_.GetValue("DisplayName") \
  $_.GetValue("DisplayVersion") }
""Installed Patches"
get-winobject Win32_QuickFixEngineering | Select HotFixId,
InstalledOn
===""
ses winrm.Session('172.16.85.130', auth=
('sussurro', 'Abc123!')
r = ses.run ps(script)
print r.std_out
```

Looking at the script, the first line of our script prints out our header of "Installed Software." Then we have a complex line that gets and filters data. The Get-ChildItem will get the list of all the software in the uninstall key. We only want keys with the subkeys that will have information about our installed software, so we use the "{$_.ValueCount-gt 0" filter to indicate we only want to see items that have a ValueCount greater than 0. From there we get the DisplayName and Display Version and print those out. That will give us the software name and version for output.

Next we query the Win32_QuickFixEngineering wmi table. This table contains the list of all the patches installed, but we only want two items, the patch and the install date. We use select to just pull those items out, and then are are output to the screen.

As a result, we should have output similar to that shown in Fig.6.12. A live host will likely have much more information in it, as it will include only software that has been installed by the user but also additional items that have been installed as part of the OS, entries from patches, and so on.