```
for i in X_val.index:
    print(i)

    for col in X_val.columns:
        print(f"{col} = {X_val[col][i]}")

    print(f"y_real = {y_val[i]}, y_pred = {y_pred[i]}, error = {y_val[i] - y_pred[i]}")

    print()
```

```
91691
Gender = 0.0
Customer Type = 0.0
Age = 0.17335842271161097
Type of Travel = 0.0
Class = 0.0
Flight Distance = 2.05114135755668508
Inflight wifi service = 4
Departure/Arrival time convenient = 4
Ease of Online booking = 3
Gate location = 4
Food and drink = 5
Online boarding = 5
Seat comfort = 4
Inflight entertainment = 5
On-board service = 5
Leg room service = 5
Baggage handling = 5
Checkin service = 3
Inflight service = 5
```

I can now visualize the results using my favorite scatter contour plot.

![](bbox=[0.172, 0.55, 0.887, 0.831])