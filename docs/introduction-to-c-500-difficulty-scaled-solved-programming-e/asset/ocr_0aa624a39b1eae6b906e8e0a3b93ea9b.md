# 27 • Application Example 865

```
int main()
{
    int CRV, index, num, sel;
    Msg msg;

    CRV = 100; // Just, an initial value.
    while(1) {
        cout << "\noperations\n";
        cout << "--------------------\n";

        cout << "\1. Establish Call\n";
        cout << "\2. Release Call\n";
        cout << "\3. Show Calls\n";
        cout << "\4. Exit\n";

        cout << "\nenter choice: ";
        cin >> sel;

        switch(sel) {
            case 1:
                msg.code = SETUP;
                msg.CRV = CRV; // Call identifier.
                CRV++; /* For simplicity, the CRV of each call is
increased by one. */
                prctl.handle_up_msg(&msg); /* In a real
application, the user enters information related to the call, such as the
phone number of the called user. */
                break;
            case 2:
                cout << "\nEnter CRV of the call to be released: ";
                cin >> num;
                index = prctl.find_call(num); /* We find the
call, that is, with the same CRV as the one entered by the
user. */
                if(index != -1) {
                    msg.code = RELEASE;
                    msg.CRV = num;
                    prctl.call_index = index;
                    prctl.handle_up_msg(&msg); /* Activate the
call release procedure. */
                }
                else {
                    cout << "\Non existing call\n";
                    break;
            case 3:
                prctl.show();
                break;
            case 4:
                return 0;
        }
    }
}
```