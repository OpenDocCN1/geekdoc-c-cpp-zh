```
cout<<"stack is not empty";
s1.push(10);
s1.push(5);
//s1.push(7);
//s1.push(14);
cout<<"total    number    of    elements    in    stack    are:"<<s1.count_elements()<<endl;
s1.push(90);
//s1.push(299);
cout<<" element(s) in the stack are:"<<endl;
s1.display();
n=s1.pop();
cout<<" element pop is "<<n<<endl;
n=s1.pop();
cout<<" element pop is "<<n<<endl;
n=s1.pop();
cout<<" element pop is "<<n<<endl;
if(s1.isempty())
cout<<"stack under flow"<<endl;
else
{
n=s1.pop();
cout<<" element pop is "<<n<<endl;
}
getch();
return 0;
}
```

# 5.6 APPLICATION OF STACK

Stack is applied in variety of applications. In majority of applications, usage of stack is either explicit or implicit. For instance, in non-recursive traversal of a tree this data structure is explicitly used. In the recursion, it is implicitly used by the program. Stack is widely utilized in the application such as parenthesis matching, infix to postfix conversion, evaluation of complex expression etc. Applications utilizing stack have been discussed in the upcoming sub-section.