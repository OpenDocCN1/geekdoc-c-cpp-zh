
algorithm and domain independent, which may be applied to a wide range of learning tasks. One of the many possible applications to the field of IR might be solving a basic problem faced by an IRS: the need to find the groups that best describe the documents, and allow each other to place all documents by affinity. The problem that arises is in the difficulty of finding the group that best describes a document, since they do not address a single issue, and even if they did, the manner the topic is approached can also make it suitable for another group. Therefore, this task is complex and even subjective as two people could easily assign the same document to different groups using valid criteria.

Clustering is an important tool in data mining and knowledge discovery because the ability to automatically group similar items together enables one to discover hidden similarity and key concepts [10]. This enables the users to comprehend a large amount of data. One example is searching the World Wide Web, because it is a large repository of many kinds of information, many search engines allow users to query the Web, usually via keyword search. However, a typical keyword search returns a large number of Web pages, making it hard for the user to comprehend the results and find the information that really needs. A challenge in document clustering is that many documents contain multiple subjects.

This paper presents a GA applied to the field of documentation, the algorithm improved itself by refining its parameters, offering a balance between intensification and diversity that ensures an acceptable optimal fitness along an unsupervised document cluster.

## 2. Documentary base

In this study we make use of two collections, the “Reuters 21578” collection and a Spanish documentary base that includes editorials of “El Mundo” from 2006 and 2007 in an open access format.

Reuters Documentary Base consists of real news wires that appeared in Reuters in 1987, this collection is becoming a standard within the domain of the automatic categorization of documents and is used by many authors in this area. The collection consists of 21578 documents distributed in 22 files. We developed a documentary process named NZIPF [6] [11] to generate documentary vectors that feed the system.

The documentary process consists of several stages of document processing, each of which represents a process that was developed on the base document to obtain documentary vectors more efficiently.

The first step is the so-called process of Filter whose main objective is to define the documents of the documental base with the purpose of having documents that belong to a single category, that which will allow to have a smaller complexity in the treatment of the documents. Then, the purpose of the process of Zoning on the documents is the one of obtaining the free text of each document. Next, we use a process of Stop List, we extract the terms of the text of the document where each one of the extracted words will be compared with a list of empty words that will eliminate the words that don’t have interest or they lack own meaning. Then, the words will be able to suffer a process of cutting of their roots “Stemming”, in our case, we have implemented and used an algorithm of Porter in English and another in Spanish. In this step, the frequency of the obtained terms is calculated, for all the documents of our documental base, with the purpose of being able to know which terms are more used in each one of the documents; and then with this information to be able to carry out a process of selection of those terms that are more representative. The following step will consist on selecting those terms with bigger discriminatory power to proceed to its normalization. We apply the law of Zipf, we calculate the Point of Goffman [3] and the transition area that it allows us to obtain the terms of the documental base. Finally, we assign weight using a function IDF (Inverse Document Frequency) developed by Salton [4] that uses the frequency of a word in the document. After all these processes, we obtain the characteristic vectors of documents in the document collection.

The process is outlined in Figure 1.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_136_0.png)

Fig. 1. Documentary process conducted

On the other hand, within the testing environment there should be a user to provide documents that are meant to be grouped. The role of the user who provides documents will be represented by the samples of "very few (20), few (50), many (80) and enough (150)" documents, with the requirement that belonged to only two categories of Reuters or distribution of Editorials in Spanish represented by their feature vectors stemmer. Figure 2 shows the documentary environment [10] that we used for the experiments, it is important to note that, unlike the algorithms of the type monitored, where the number of obtained groups needs to be known, our algorithm will evolve to find the most appropriate structure, forming the groups by itself.

Due to the nature of simulation of GA, its evolution is pseudo-random, this translates into the need for multiple runs with different seeds to reach the optimal solution. The generation of the seed is carried out according to the time of the system. For this reason, the experiments with GA were made by carrying out five executions to each of the samples taken from experimental collections [1]. The result of the experiment will be the best fitness obtained and their convergence. To measure the quality of the algorithm, the best solution obtained and the average of five runs of the GA must be analyzed.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_137_0.png)

Fig. 2. Experimental environment used in the tests with the GA.

## 3. Genetic algorithm for document clustering

### 3.1 Individuals

The population consists of a set of individuals, where each of them is made of a linear chromosome that is represented through a tree structure (hierarchical structure). An individual shall be formed on a binary tree structure *cluster all documents* prepared at the top, where each document consists of a *feature vector*. The vector will consist of the weighted values of the frequencies of the stemmer terms that have been selected to implement the document processing scheme [4]. This representation will be attempted to evolve so that the chromosome will undergo genetic changes and find the groups 'Clusters' more appropriate for all documents of the IRS. Within the root node we will have our fitness function (*fitness*) that measures the quality of the resulting clustering. Depending on the number of documents that need to be processed and the depth (height) of the tree you want to create, chromosome may be of variable length.

The Figure 3 shows the initial generation (0), a scheme of tree-based representation is adopted in order to allow the encoding of sufficiently complex logical structures within a chromosome. The search area for the GA is the space of all possible trees that can be generated, resulting from the whole relevant functions and terminals. This way we can evolve individuals of various shapes and sizes [8], allowing evolution to decide what are the best settings.

Although the initial population is random, there is a defined set of parameters governing the establishment of such individuals. For example, *there should not be created in the initial set two equal individuals*, for this, production rules are created to ensure the compliance with this condition. The above-mentioned rules require that the building grammar of each individual node takes place in preorder.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_138_0.png)

Fig. 3. Initial Population of Individuals GA (generation "0")

### 3.2 Production operators

The production operators are applied to each new generation. One or two individuals can be taken to produce new individuals for next generation by applying the transformations imposed by the operator. Both mutation operators and crossover will be implemented indistinctly. Both operators depend on a mutation probability and / or crossover that is assigned to GA [7].

*A mutation operator is applied on nodes (documents), selecting an individual from the population using the tournament method, and then randomly select a pair of terminal nodes of that individual to mutate its terminal nodes, generating a new individual transposing the nodes that have been chosen (see figure 4).*

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_138_1.png)

Fig. 4. Basic mutation operator applied to terminal
