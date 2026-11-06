```
```
cout << "All Finished!" << endl;
return 0;
}
```
```

This code runs while i is less than or equal to 5. Thus, the output of this appli-cation is

```
```
0
1
2
3
4
5
All Finished!
```
```

Notice that you must declare i outside the while loop using int i = 0;. If you were to try to declare the while loop using while (int i <= 5), the compiler would complain.

The while loop is handy if you don't have a particular number of times you need the loop to run. For example, consider a situation in which your application is reading data from the Internet. Unless you control the Internet data source, you don't know how much data it can provide. (Many other situations can arise in which you don't know how much data to read, but Internet applications com-monly experience this problem.) Using a while loop, the code can continue read-ing data until your application has read it all. The Internet data source can simply stream the data to your application until the data transfer is complete.

Often, for this kind of situation, you create a Boolean variable called done and start it out as false. The while statement is simply

```
```
while (!done)
```
```

This line translates easily to English as "while not done, do the following." Then, inside the while loop, when the situation happens that you know the loop must finish (such as the Internet data source has no more data to read), you set

```
```
done = true;
```
```