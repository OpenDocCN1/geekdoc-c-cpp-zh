![](bbox=[0.29, 0.09, 0.84, 0.25])

# Putting It All Together

A TabControl inside a dialog-based window manages the displayed information. The TabPages are created dynamically from information sent by the debugged game. For an example of a TabControl and TabPages, see figure 1.12.2.

![](bbox=[0.31, 0.46, 0.82, 0.61])

After starting the debug logger, we will try to connect to the logged game we want to log. Once connected, the logged game will send the TabPages name that it wants to register with the logger. These names will have an index associated, and only the index will be sent in further communication. Then it will send the list of the names it wants to have logged along with the type of representation that should be used and specific data if needed (such as a range, for graphs).

Once it is connected and initialized, the logger will then start to receive the data. Each data packet contains the TabPage index, the ValueName index, and the actual data. A quick lookup tells us exactly which part of a specific page to update. The data representation class takes care of displaying the data as intended.