| Action | Action Argument | Action Argument Setting |
|---|---|---|
| Echo | Echo On | Yes |
|  | Status Bar Text | <Leave Blank> |
| SetWarnings | Warnings On | Yes |
| DisplayHourglassPointer | Hourglass On | No |
| MessageBox | Message | Contacts and Products have been archived. |
|  | Beep | Yes |
|  | Type | Information |
|  | Title | Finished Archiving |

The heart of the macro is the four OpenQuery actions that run the four action queries. qryDeleteContactsBackup and qryDeleteProductsBackup clear the contents of tblContacts_Backup and tblProducts_Backup so that the current data can be copied into them. qryAppendContactsBackup and qryAppendProductsBackup append data from tblContacts and tblProducts into the backup tables.

As you look in Figure 22.8, you will note the warning icons next to a few of the actions in the macro (specifically SetWarnings and Echo). These icons simply indicate that the associated actions are potentially unsafe and may require a closer look.

Here's a closer look at the actions this macro performs:

+   - DisplayHourglassPointer: This action changes the cursor to an hourglass or a pointer using the Hourglass On argument. For macros that may take a while to run, set this argument to Yes at the beginning of the macro and to No at the end of the macro. Be sure not to forget to set Hourglass Off at the conclusion of the macro; otherwise, the hourglass cursor stays on indefinitely.

+   - SetWarnings: This action turns the system messages on or off using the Warnings On argument. When running action queries, you'll be prompted to make sure you want to run the action query, asked whether it's okay to delete these 58 records, and then asked again for the next action query. Set Warnings On to No at the beginning of the macro to turn these messages off. Setting Warnings On to No has the effect of automatically clicking the default button of the warning (usually OK or Yes). Don't forget to set warnings back to Yes at the end of the macro. Once warnings are turned off, the user won't get confirmation messages from Access on important actions like record deletions until warnings are re-enabled.

+   - Echo: In effect, the Echo command "freezes" the screen so that the user isn't aware of activities performed by the macro. Set the Echo On argument to No if you want to hide the results of the macro or Yes if you want to show the results. Set the Status Bar Text argument to give the user an indication of what's happening. This is useful in longer-running macros to know where in the process the macro is.