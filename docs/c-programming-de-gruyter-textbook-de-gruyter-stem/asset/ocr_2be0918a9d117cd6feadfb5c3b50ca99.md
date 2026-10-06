```
{
int gamestatus,sum,mypoint;
unsigned seed;
cout<<"Please enter an unsigned integer:";
cin>>seed; //Input the seed for the random number
rand(seed); //Pass the seed to rand()
sum=rolldice(); //The first round, roll the dice and get the
//point total

switch(sum)
{
case 7: //Win if the point total is 7 or 11, status=1
case 11:
    gamestatus=1;
    break;
case 2: //Lose if the point total is 2, 3 or 12, status=2
case 3:
case 12:
    gamestatus=2;
    break;
default:
    //Otherwise, continue the game, record the player's
    //point, and set status=0
    gamestatus=0;
    mypoint=sum;
    cout<<"point is "<<mypoint<<endl;
break;
}

while(gamestatus==0) //Go to the next round if status = 0
{
sum=rolldice();
if(sum==mypoint) //Win if the point total is equal to the
//player's point, set status=1
    gamestatus=1 ;
else
    if ( sum==7) //Lose if the point total is 7, set status=2
    gamestatus=2;
}
//When the status is not 0, the loop above ends, and the following
if(gamestatus==1)
    cout<<"player wins\n";
else
    cout<<"player loses\n";
}
```