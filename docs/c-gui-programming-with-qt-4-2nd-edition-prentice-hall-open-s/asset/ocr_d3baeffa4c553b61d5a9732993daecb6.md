# Handling X11 Session Management

When we log out on X11, some window managers ask us we want to save the session. If we say yes, the applications that were running are automatically restarted the next time we log in, with the same screen positions and ideally, with the same state as they had when we logged out. An example of this is shown in Figure 23.7.

# Figure 23.7. Logging out on KDE

![](bbox=[0.01, 0.218, 0.475, 0.462])

The X11-specific component that takes care of saving and restoring the session is called the session manager. To make a Qt/X11 application aware of the session manager, we must reimplement QApplication::saveState() and save the application's state there.

Microsoft Windows and some Unix systems offer a different mechanism called hibernation. When the user puts the computer into hibernation, the operating system simply dumps the computer's memory onto disk and reloads it it wakes up. Applications do not need to do anything or even be aware that this happens.

When the user initiates a shutdown, we can take control just before the shutdown occurs by reimplementing QApplication::commitData(). This allows us to save any unsaved data and to interact with the user if required. This part of session management is supported on both X11 and Windows.

We will explore session management by going through the code of the session-aware Tic-Tac-Toe application shown in Figure 23.8. First, let's look at the main() function:

```
int main(int argc, char *argv[])
{
    Application app(argc, argv);
    TicTacToe toe;
    toe.setObjectName("toe");
```