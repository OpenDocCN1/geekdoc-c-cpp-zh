```
break;
    }    else    // else2
    {
        if(Curr->exp < NewTerm->exp)    //if 3
        {
            if(Curr == Head)    // if 4
            {
                NewTerm->link = Head;
                Head = NewTerm;
                break;
            }
            else    // else 4
            {
                prev->link = NewTerm;
                NewTerm->link = Curr;
                break;
            }
        }    // end if 3
    }    // end else 2
    prev = Curr;
    Curr = Curr->link;
    }    // end of while
    if(Curr == Null)    // add at end
    {
        prev->link = NewTerm;
        Tail = NewTerm;
    }    // end of else
}    // end of function

void main()
{
    Poly P1, P2, P3;
    P1.Create();
    P1.Display();
    P2.Create();
    P2.Display();
    P3 = P1.PolyMult(P2);
    P3.Display();
    getch();
}
```