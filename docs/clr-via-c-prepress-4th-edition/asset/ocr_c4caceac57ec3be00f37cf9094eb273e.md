<table>
<tr><td>Time-Critical</td><td>15</td><td>15</td><td>15</td><td>15</td><td>15</td><td>31</td></tr>
<tr><td>Highest</td><td>6</td><td>8</td><td>10</td><td>12</td><td>15</td><td>26</td></tr>
<tr><td>Above Normal</td><td>5</td><td>7</td><td>9</td><td>11</td><td>14</td><td>25</td></tr>
<tr><td>Normal</td><td>4</td><td>6</td><td>8</td><td>10</td><td>13</td><td>24</td></tr>
<tr><td>Below Normal</td><td>3</td><td>5</td><td>7</td><td>9</td><td>12</td><td>23</td></tr>
<tr><td>Lowest</td><td>2</td><td>4</td><td>6</td><td>8</td><td>11</td><td>22</td></tr>
<tr><td>Idle</td><td>1</td><td>1</td><td>1</td><td>1</td><td>1</td><td>16</td></tr>
</table>

For example, a Normal thread in a Normal process is assigned a priority level of 8. Because most processes are of the Normal priority class and most threads are of Normal thread priority, most threads in the system have a priority level of 8.

If you have a Normal thread in a high-priority process, the thread will have a priority level of 13. If you change the process's priority class to Idle, the thread's priority level becomes 4. Remember that thread priorities are relative to the process's priority class. If you change a process's priority class, the thread's relative priority will not change, but its priority number will.

Notice that the table does not show any way for a thread to have a priority level of 0. This is because the 0 priority is reserved for the zero page thread and the system does not allow any other thread to have a priority of 0. Also, the following priority levels are not obtainable: 17, 18, 19, 20, 21, 27, 28, 29, or 30. If you are writing a device driver that runs in kernel mode, you can obtain these levels; a user-mode application cannot. Also note that a thread in the Realtime priority class can't be below priority level 16. Likewise, a thread in a priority class other than Realtime cannot be above 15.

**Note** The concept of a process priority class confuses some people. They think that this somehow means that Windows schedules processes. However, Windows never schedules processes; Windows only schedules threads. The process priority class is an abstract concept that Microsoft created to help you rationalize how your application compares with other running applications; it serves no other purpose.

**Important** It is best to lower a thread's priority instead of raising another thread's priority. You would normally lower a thread's priority if that thread was going to execute a long-running compute-bound task like compiling code, spell checking, spreadsheet recalculations, etc. You would raise a thread's priority if the thread needs to respond to something very quickly and then run for a very short period of time and go back to its wait state. High-priority threads should be waiting for something most of their life so that they do not affect the responsiveness of the whole system. The Explorer thread that responds to the user pressing the Windows key on the keyboard is an example of a high-priority thread. When the user presses this key, Explorer preempts other lower-priority threads immediately and displays its menu. As the user navigates the menu, Explorer's thread responds to each keystroke quickly, updates the menu, and then stops running until the user continues navigating the menu.

Normally, a process is assigned a priority class based on the process that starts it running. And most