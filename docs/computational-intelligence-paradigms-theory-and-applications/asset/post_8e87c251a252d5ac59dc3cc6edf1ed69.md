
## Training Algorithm

The weights and the learning rate are set initially. The input vectors to be clustered are presented to the network. When the input vectors are presented, the winner unit is calculated either by Euclidean distance method or sum of products method based on the initial weights. Based on the winner unit selection, the weights are updated for that particular winner unit using competitive learning rule as discussed earlier. An epoch is said to be completed once all the input vectors are presented to the network. By updating the learning rate, several epochs of training may be performed.

The pseudocode of the training algorithm of the SOM network is shown below:

```
Initialize topological neighborhood parameters
Initialize learning rate
Initialize weights
While not stopping condition do
    For each input vector x
        For each i, compute squared Euclidean
            distance
                D(j) = ∑ (wᵢⱼ−xᵢ)², i=1 to n and j=1 to m
        Find index J, when D(j) is minimum
        For all units J, with specified neighborhood
        of J,
            and for all i,
                update the weights to
                    wᵢⱼ(new) = wᵢⱼ(old) + α [xᵢ−wᵢⱼ(old)]
    End For
    Update the learning rate
    Reduce the radius of topological neighborhood
    at specified times
    Test the stopping condition
End While
End
```

The map function occurs in two phases:

- Initial formation of perfect (correct) order
- Final convergence

The second phase takes a longer duration than the first phase and requires a small learning rate. The learning rate is a slowly decreasing function of time and the radius of the neighborhood around a cluster unit also decreases as the clustering process goes on. The initial weights are assumed with random values. The learning rate is updated by, α (t+1) = 0.5 α (t).

## 4.5 Applications Areas of ANN

Artificial neural networks are going through the change that happens once a concept departs the academic environment and is thrown into the harsh world of users who merely wish to get a job arranged. Several networks that are being designed recently are statistically quite exact but they still leave a defective impression with users who anticipate computers to solve their problems absolutely. These networks could be 85% to 90% accurate. Regrettably, a couple of applications tolerate that level of error.

While researchers continue to work on improving the accuracy of their “creations,” some explorers are finding uses for the current technology.

In reviewing this state of the art, it is hard not to be overcome by the bright promises or tainted by the undeceived realities. Presently, neural networks are not the user interface which translates spoken words into instructions for a machine, but someday they will be. Someday, VCRs, home security systems, CD players, and word processors will simply be activated by voice. Touch screen and voice editing will replace the word processors of today while bringing spreadsheets and data bases to a level of usability pleasing to most everyone. But for now, neural networks are simply entering the marketplace in niches where their statistical accuracy is valuable as they await what will surely come.

Many of these niches indeed involve applications where answers are nebulous. Loan approval is one. Financial institutions make more money by having the lowest bad loan rate they can achieve. Systems that are “90% accurate” might be an improvement over the current selection process. Indeed, some banks have proven that the failure rate on loans approved by neural networks is lower than those approved by some of their best traditional methods. Also, some credit card companies are using neural networks in their application screening process.

This latest method of looking into the future by examining past experiences has rendered its own independent problems. One of the major problems is to provide a reason behind the computer-generated answer, such as to why a particular loan application was denied. As mentioned throughout this chapter, the inner workings of neural networks are “black boxes.” The explanation of a neural net and its learning has been difficult. To alleviate this difficult process, a lot of neural net tool developers have provided programs which explain which input through which node dominates the decision making process. From that information, experts in the application should be able to infer the reason that an exceptional piece of data is crucial.

Besides this filling of niches, neural network work is progressing in other more promising application areas. The following section of this chapter goes through some of these areas and briefly details the current work. This is done to help stimulate within the reader the various possibilities where neural networks might offer solutions, possibilities such as language processing, character recognition, image compression, pattern recognition, among others.

### 4.5.1 Language Processing

Human language users perform differently from their linguistic competence, that is from their knowledge of how to communicate correctly using their language. Natural language processing is an application reinforced by the use of association of words and concepts, implemented as a neural network. A single neural network architecture is capable of processing a given sentence, and outputs a host of language processing predictions: part-of-speech tags, chunks, named entity tags, semantic roles, semantically similar words, and the likelihood that the sentence makes sense grammatically and semantically using a language model.

Several researchers belonging to various universities are researching how a computer could be programmed to respond to spoken commands using the artificial neural networks. Natural language processing (NLP) has become the main-stream of research with neural networks (NNs), which are powerful parallel distributed learning/processing machines and they play a major role in several areas of NLP.

Presently, as reported by the academic journals, most of the hearing-capable neural networks are trained to only take one talker. These one-talker, isolated-word recognizers can recognize only a few hundred words. But when there is a pause between each word, then the neural networks can recognize more number of words.

A few investigators are touting even bigger potentialities, but due to the expected reward the true progress, and methods involved, are being closely held. The most highly touted, and demonstrated, speech-parsing system comes from the Apple Corporation. That network, according to an April 1992 Wall Street Journal article, is capable of recognizing almost any person's speech through a limited vocabulary.

### 4.5.2 Character Recognition

The recognition of optical characters is known to be one of the earliest applications of Artificial Neural Networks, which partially emulate human thinking in the domain of artificial intelligence. Recognition of either handwritten or printed characters is a major area in which neural networks are providing optimal solutions. Multilayer neural networks are used to recognize characters which is a vital application in areas like banking, etc. The main issue in character recognition is the trade-off between cost and benefits such as accuracy and speed. Neural networks provide a method for combining independently trained characters to achieve higher performance at relatively low cost.

The greatest amount of recent research in the domain of character recognition is targeted at scanning oriental characters into a computer. Presently, these characters require four or five keystrokes each. This complicated process stretches the task of identifying a page of text into hours of drudgery.

### 4.5.3 Data Compression

In neural networks, when the number of hidden units is less when compared to the input and output units, then the neurons of the middle layer are capable of data compression. Researchers have proved that neural networks can do real-time compression and decompression of data. These networks are auto-associative in that they can reduce eight bits of data in the input layer to three in the hidden layer and then reverse that process upon restructuring to eight bits again in the output layer. While compressing there is no loss in the information. Some of the major applications of data compression are multispectral lossless image compression, pattern recognition, lossy or lossless compression, video compression, handwritten numeral classification, edge detection, and magnetic resonance image compression.

### 4.5.4 Pattern Recognition

Pattern recognition is a very old application of neural networks and it has been studied in relation to many different (and mainly unrelated) applications, such as classifying patterns by shape, identifying fingerprints, identifying tumors, handwriting recognition, face recognition, coin recognition, etc. The majority of these applications are concerned with problems in pattern recognition, and make use of feed-forward network architectures such as the multi-layer perceptron and the radial basis function network. According to the perspective of pattern recognition, neural
