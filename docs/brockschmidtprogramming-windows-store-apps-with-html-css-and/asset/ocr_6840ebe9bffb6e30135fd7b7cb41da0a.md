The completed handler for `join` then receives an array that contains all the results of the individual promises. This handler then simply iterates that array, calling the sample's `outputResultGroup` and `outputItems` methods for each set, which just build up a DOM tree for the display. The results for my pictures library with `groupByTag` are as follows (revealing a small extent of my travels!):

A-Picture Tags/Places/Overseas/Egypt (3)
2008-02-29_009.JPG
2008-02-29_020.JPG
2008-02-29_035.JPG
A-Picture Tags/Places/Overseas/India (3)
159-16 Taj Mahal, Agra, India 9-98.JPG
159-37 Taj Mahal, Agra, India 9-98.JPG
160-7 Taj Mahal, Agra, India 9-98.JPG
A-Picture Tags/Places/States/Oregon/Outdoors/Oregon Coast (1)
122-10 Sunset, Pacific Beach, WA 6-95.JPG
A-Picture Tags/Places/States/Southwest/Arizona (3)
84-13 Sunset Crater and Tree, AZ 5-93.JPG
85-7 Ruins at Sunset, Wupatki NM, AZ 5-93.JPG
85-12 Wupatki Ruins Sunset, AZ 5-93 (2).jpg
A-Picture Tags/Places/States/Southwest/Colorado (1)
237-26 Flower Close-Ups, Rocky Mountain NP, CO 6-06.JPG
A-Picture Tags/Places/Family/Ocean Shores (28)
226-5 Seagulls in Sunset, Ocean Shores, WA 9-03.JPG
226-34 Sunset, Ocean Shores, WA 9-03.JPG
227-11 Sunset, Ocean Shores, WA 9-03.JPG

As for scenario 3 of the sample, that brings us into the matter of query options, which are discussed in the next section.

# Custom Queries

Now that we've seen the basics of enumerating folder contents with common queries and processing their results, we're ready to look at the full query capabilities offered by WinRT wherein you construct a custom query from scratch using a `QueryOptions` object. (The common queries are just shortcuts for typical cases to save you the trouble.) A custom query basically gives you all the capabilities that you have through the search features of the desktop Windows Explorer, using whatever Windows Properties you require.

As with the common queries, not all locations support custom queries, so once you've built the `QueryOptions` you want to call `StorageFolder.areQueryOptionsSupported` with that object. If it returns `true`, you can proceed. If you attempt to query a folder with unsupported options, expect a "parameter is incorrect" exception.

Something else you might want to know ahead of time is whether the folder itself has been indexed, which greatly affects the potential speed of the query. You do this through `StorageFolder.getIndexedStateAsync`. This results in an `IndexedState` value: `notIndexed`, `partiallyIndexed`, `fullyIndexed`, and `unknown`. Do note a fully indexed folder could yet contain nonindexed folders, but