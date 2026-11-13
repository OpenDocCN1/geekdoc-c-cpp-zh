
## 3.4 Programs Related to Sparse Matrix

### Program for Array Representation of Sparse Matrix

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
//Driver program
int main()
{
 int arr[10][10],i,j,row,col,count=0,k=0,sp[15][3];
 //ask user about the number of rows and columns sparse matrix
 cout<<"\nENTER HOW MANY ROWS AND COLUMNS";
 //read row and col
 cin>>row>>col;
 //loop to read the normal matrix
 for(i=0;i<row;++i)
 {
 for(j=0;j<col;j++)
 {
 cout<<endl<<"Enter a number";
 cin>>arr[i][j];
 }
 }
 //loop to print the normal matrix that read from user
 cout<<"\nTHE ENTERED ARRAY ELEMENTS ARE\n";
 for(i=0;i<row;++i)
 {
 for(j=0;j<col;++j)
 {
 cout<<setw(4)<<arr[i][j];
 cout<<endl;
 }
 }
 //loop to count the number of non zero elements in the matrix
 for(i=0;i<row;++i)
 {
 for(j=0;j<col;++j)
 {
 if(arr[i][j]!=0)//condition for non zero elements
 count++;//increase the count
 }
 //set the first row of sparse matrix
 sp[0][0]=row;
 sp[0][1]=col;
 sp[0][2]=count;
 k=1;//k points to second row of sparse matrix
 //loop to fill the other rows of sparse matrix
 for(i=0;i<row;++i)
 {
 for(j=0;j<col;++j)
 {
 if(arr[i][j]!=0)
 {
 sp[k][0]=i;
 sp[k][1]=j;
 sp[k][2]=arr[i][j];
 k++;
 }
 }
 }
 }
/*print the sparse matrix */
cout<<"\nTHE SPARSE MATRIX IS\n";
for (i=0;i<count;i++)
{
for (j=0;j<3;j++)
cout<<" "<<sp[i][j];
cout<<endl;
}
}
```

### OUTPUT

```
ENTER HOW MANY ROWS AND COLUMNS
4
3
Enter a number
0
0
Enter a number
0
Enter a number
0
Enter a number
3
Enter a number
0
Enter a number
5
Enter a number
0
Enter a number
6
Enter a number
0
Enter a number
0
Enter a number
8
THE ENTERED ARRAY ELEMENTS ARE
0 0 0
0 0 0
5 0 6
0 0 8
THE SPARSE MATRIX IS
4 3 4
1 1 3
2 0 5
2 2 6
3 2 8
```

### Transpose of a Sparse Matrix

```cpp
#include<iostream>
#include<conio.h>
using namespace std;
int main()
{
int arr[10][10],i,j,row,col,count=0,k=0,sp[15][3],tran[10][3];
//ask user about the number of rows and columns sparse matrix
cout<<"\nENTER HOW MANY ROWS AND COLUMNS";
//read row and col
cin>>row>>col;
//loop to read the normal matrix
for(i=0;i<row;i++)
for(j=0;j<col;j++)
{
cout<<endl<<"Enter a number";
cin>>arr[i][j];
}
//loop to print the normal matrix that read from user
cout<<"\nTHE ENTERED ARRAY ELEMENTS ARE\n";
for(i=0;i<row;i++)
for(j=0;j<col;j++)
cout<<setw(4)<<arr[i][j];
cout<<endl;
}
//loop to count the number of non zero elements in the matrix
for(i=0;i<row;i++)
for(j=0;j<col;j++)
if(arr[i][j]!=0)//condition for non zero elements
count++; //increase the count
//set the first row of sparse matrix
sp[0][0]=row;
sp[0][1]=col;
sp[0][2]=count;
k=1;//k points to second row of sparse matrix
//loop to fill the other rows of sparse matrix
for(i=0;i<row;i++)
for(j=0;j<col;j++)
{
if(arr[i][j]!=0)
{
    sp[k][0]=i;
    sp[k][1]=j;
    sp[k][2]=arr[i][j];
    k++;
    }
    }
    }
/*print the sparse matrix */
cout<<"\nTHE SPARSE MATRIX IS\n";
for(i=0;i<count;i++)
    {
    for(j=0;j<3;j++)
    cout<<sp[i][j];
    cout<<endl;
    cout<<endl;
    }
    }
/**TRANSPOSE**/
tran[0][0]=col;
tran[0][1]=row;
tran[0][2]=count;
k=1;
for(i=0;i<col;i++)
    for(j=1;j<count;j++)
    {
    if(sp[j][1]==i)
    {
    tran[k][0]=sp[j][1];
    tran[k][1]=sp[j][0];
    tran[k][2]=sp[j][2];
    k++;
    }
    }
    cout<<"\nTRANSPOSE OF THE SPARSE MATRIX\nIS\n";
for(i=0;i<count;i++)
    {
    for(j=0;j<3;j++)
    cout<<setw(5)<<tran[i][j];
    cout<<endl;
    }
}
```

### OUTPUT

![](img/1faaa0256577c74e8a61f42967760aa8_65_0.png)

## 3.5 Why to Use Sparse Matrix Instead of Simple Matrix?

- Storage: There are lesser non-zero elements than zeros and thus lesser memory can be used to store only those non-zero elements.

- Computing time: Computing time can be saved by logically designing a data structure traversing only non-zero elements.

## 3.6 Drawbacks of Sparse Matrix

### Memory Drawbacks of a Sparse Matrix

Every element of a program array takes up memory and a sparse matrix can end up taking unnecessary amounts of memory space. For example, a 10x10 array can occupy 10 x 10 x 1 byte (assuming 1 byte per element) = 100 bytes. If a majority of these elements say 70 of 100, are zeroes, then 70 bytes of space is essentially wasted. Sometimes large sparse matrices are too big to fit into memory.

### Computational Drawbacks of a Sparse Matrix

Performing algorithmic computations (like matrix multiplication, for example) takes up a lot of unnecessary time for each zero computation. Anything multiplied by zero is zero, but this operation still has to be performed which is seen as a waste of computational time.

A sparse matrix can be compressed and memory reduction can be achieved by storing only the non-zero elements. However, this will also require programming additional structures to recover the original matrix when elements have to be accessed, but overall a compressed sparse matrix can ultimately increase computational speed.

Sparse matrices are very common in machine learning algorithms. Now that your question ‘what is sparse matrix’ is answered, let’s understand some examples and its uses.

## 3.7 Sparse Matrix and Machine Learning

As mentioned earlier, sparse matrices are a common occurrence in Machine Learning algorithms.

### 1. In Data Storage

- (a) In a movie application like Netflix, the array that stores the check of which movies are watched and not watched in a catalog.

- (b) In e-commerce programs, data that represents the products purchased and not purchased by a user.

- (c) In a music app, the count of songs listened and not listened to by a user.

### 2. In Data Preparation

Sparse matrices are often seen in encoding schemes, which are used for data preparation.

- Examples:
- (a) One-hot encoding, which is used to represent categorical data as sparse binary vectors.
- (b) Count encoding, which is used in the representation of the frequency of words in a document.
- (c) TF-IDF encoding, which is used in representing frequency scores of words in the vocabulary.

### 3. Machine Learning Study Areas

Sometimes, machine learning study areas require the development of specialized methods to address sparse matrices as input data. Examples are:

- (a) Natural Language Processing when working with text documents
- (b) Recommendation systems for product catalog programs.
- (c) In Computer Vision when scanned images have a lot of dark or black pixels.

### Different Methods of Sparse Matrix Representation & Compression

Storing a sparse matrix takes up unnecessary space and increases computational time. There are ways for sparse matrix representation in a 'compressed' format, which improves its efficiency.

## 3.8 Questions

- 1. What is a sparse Matrix?
- 2. Write some implementation areas of sparse matrix.
- 3. How to represent sparse matrix.
- 4. Differentiate with suitable example about the representation of sparse matrix.
- 5. Is it more beneficial to use sparse matrix than dense matrix? Explain your answer.
- 6. What are the limitations of sparse matrix?
- 7. Specify a few limitations of sparse matrix.

## Concepts of Class

## 4.1 Introduction to CLASS

Like structure the class is also a user defined data type or Abstract Data Type (which derives/combines the properties of different data types into a single unit), which combines both the data members and member functions into a single unit. The Object oriented properties like Data encapsulation and Data Hiding is fully supported by the class.

Like structure the class has also its declaration and before its use we must have to declare it. The declaration of the class is very simple except that all the members of the class can be arranged in different sections (block) to achieve the data hiding.

The main purpose of C++ programming is to add object orientation to the C programming language and classes are the central feature of C++ that supports object-oriented programming and are often called user-defined types.

A class is used to specify the form of an object and it combines data representation and methods for manipulating that data into one neat package. The data and functions within a class are called members of the class.

When you define a class, you define a blueprint for a data type. This does not actually define any data, but it does define what the class name means, that is, what an object of the class will consist of and what operations can be performed on such an object.
