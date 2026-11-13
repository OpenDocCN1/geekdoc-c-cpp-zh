```
int main()
{
    sequence test; // A sequence that we'll perform tests on
    char choice; // A command character entered by the user
    cout << "I have initialized an empty sequence of real numbers." << endl;
    do
    {
        print_menu();
        choice = toupper(get_user_command());
        switch (choice)
        {
            case '!': test.start();
                break;
            case '+': test.advance();
                break;
            case '?': if (test.is_item())
                cout << "There is an item." << endl;
            else
                cout << "There is no current item." << endl;
            case 'C': if (test.is_item())
                cout << "Current item is: " << test.current() << endl;
            else
                cout << "There is no current item." << endl;
            case 'P': show_sequence(test);
            case 'S': cout << "Size is " << test.size() << '.' << endl;
                break;
            case 'I': test.insert(get_number());
                break;
            case 'A': test.attach(get_number());
                break;
            case 'R': test.remove_current();
                cout << "The current item has been removed." << endl;
                break;
            case 'Q': cout << "Ridicule is the best test of truth." << endl;
                break;
            default: cout << choice << " is invalid." << endl;
        }
    } while ((choice != 'Q'));
    return EXIT_SUCCESS;
}
```