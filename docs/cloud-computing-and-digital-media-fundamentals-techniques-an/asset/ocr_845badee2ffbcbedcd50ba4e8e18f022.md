maxima over spectrograms, are then extracted from the spectrogram. These landmarks are then stored as a hash table for comparison dur- the retrieval stage.

+   Retrieval stage. During retrieval, the query obtains landmarks for comparison using the above-mentioned procedure. The system then performs an efficient table lookup to identify relevant hash entries in the hash table. Based on the difference in offset time of both the query and the database landmarks, we should be able derive the number of matched landmarks for each song. The song with the most matching landmarks is more likely to be the desired song. The system then returns a ranked list according to the matched landmark counts.

Currently, several companies provide QBSH and/or QBEE as MIR ser- vices, including SoundHound [1] (snapshot of app is shown in Figure 4.2) and Shazam [2]. Companies such as IntoNow also use QBEE to identify television programs so that extra information about the program can be used to promote related products on a second screen (i.e., mobile device).

![](bbox=[0.129, 0.545, 0.861, 0.883])

FIGURE 4.2 Snapshot of the SoundHound app.