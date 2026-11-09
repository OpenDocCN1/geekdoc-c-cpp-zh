```
Phone.Dial
BetterPhone.EstablishConnection
```

This output shows that Main's call to Dial calls the Dial method defined by Phone and inherited by BetterPhone. Then when Phone's Dial method calls the virtual EstablishConnection method, BetterPhone's EstablishConnection method is called because it overrides the virtual EstablishConnection method defined by Phone.