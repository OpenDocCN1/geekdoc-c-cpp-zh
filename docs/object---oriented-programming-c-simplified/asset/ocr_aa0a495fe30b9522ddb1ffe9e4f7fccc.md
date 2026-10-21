```
cin >> sa;
}
};
class third :public second
{
    protected :
        int ta;
    public :
        void input_t()
        {
            input_s();
            cout << "Enter the value for ta :=";
            cin >> ta;
        }
        void show()
        {
            cout << "Data of class first fa :=" << fa << endl;
            cout << "Data of class second sa :=" << sa << endl;
            cout << "Data of class third ta :=" << ta << endl;
        }
        int max()
        {
            int t1,t2;
            t1 = fa > sa ? fa : sa;
            t2 = ta > t1 ? ta : t1;
            return t2;
        }
};
void main()
{
    clrscr();
    third t;
    t.input_t();
    t.show();
    cout << "Max is " << t.max() << endl;
    getch();
}
```