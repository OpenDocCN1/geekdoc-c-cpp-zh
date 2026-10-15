satisfaction would be Y.

# Normalization

```
In [6]: from sklearn.preprocessing import StandardScaler

age_scaler = StandardScaler()
airplane['Age'] = age_scaler.fit_transform(airplane[['Age']])

flight_distance_scaler = StandardScaler()
airplane['Flight Distance'] = flight_distance_scaler.fit_transform(airplane[['Flight Distance']])
# departure_scaler = StandardScaler()
# airplane['Departure Delay in Minutes'] = departure_scaler.fit_transform(airplane[['Departure
# arrival_scaler = StandardScaler()
# airplane['Arrival Delay in Minutes'] = arrival_scaler.fit_transform(airplane[['Arrival Delay

airplane['Departure Delay in Minutes'] = airplane['Departure Delay in Minutes'].apply(lambda x

airplane['Arrival Delay in Minutes'] = airplane['Arrival Delay in Minutes'].apply(lambda x : 1
```

This is the label. Remember that this is supervised learning. I create my model and fit the data.

![](bbox=[0.19, 0.52, 0.8, 0.78])

It is always important to keep an eye not only in the accuracy. Also, remember to use the confusion matrix and the classification report.