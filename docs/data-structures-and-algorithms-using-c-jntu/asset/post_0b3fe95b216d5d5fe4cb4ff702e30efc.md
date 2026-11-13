
Pass 2: In this pass, the text character 'F' and the pattern character 'M' are compared. In this case the comparison fails. The character 'F' is not present in the set of characters of the pattern. This case is referred to as the Bad Character Shift. In the shift table, the number of shifts for the character 'F' is 9. So, the pattern 'ALGORITHM' is moved 9 characters forward.

Pass 3: In this pass, the text character 'O' and the pattern character 'M' are compared. In this case the comparison fails. But the character 'O' is present in the set of characters of the pattern. In the shift table, the number of shifts for the character 'O' is 5. So, the pattern 'ALGORITHM' is moved 5 characters forward.

Pass 4: In this pass, the text character 'A' and the pattern character 'M' are compared. In this case the comparison fails. But the character 'A' is present in the set of characters of the pattern. This case is referred as the Good Suffix Shift. In the shift table, the number of shifts for the character 'A' is 8. So, the pattern 'ALGORITHM' is moved 8 characters forward.

Pass 5: In this pass, the text character 'M' and the pattern character 'M' are compared. In this case the comparison succeeded. So, the algorithm compares the character of the Text 'H' and the character of the pattern 'H' is compared. So again the immediate previous characters of the pattern and the text are compared until all the characters are compared. Because all the characters are matched, the index of the last character match will be returned.

## Program 15.2

```cpp
// Boyer-Moore
//#include<conio.h>
#include<string.h>
#include<iostream.h>
#include<stdio.h>
int build_table(char*p)
{
int last[128];
int i;
for(i=0;i<128;i++) last[i]=-1;
for(i=0;i<strlen(p);i++)
{
last[p[i]]=i;
}
return(last);
}

int min(int a,int b)
{
if(a>b) return(b);
else return(a);
}
int search(char*t,char*p)
{
int n=strlen(t);
int m=strlen(p);
int i=m-1;
if(i>n-1)return (-1);
int j=m-1;
do{
    if(p[j]==t[i])
    if(j==0)return i;
    else {
    i--;
    j--;
    }
    else {
    i+=m-min(j,1+last[t[i]]);
    j=m-1;
    }
}while(i<=n-1);
return(-1);
}

void main(){
    char T[128],P[128];
    int index;
    clrscr();
    cout << "\nEnter Text:";
    gets(T);
    cout << "\nEnter Pattern:";cin>>P;
    index=search(T,P);
    if(index==-1)
    {
    cout<<"\nMatch Found At:"<<index;
    }
    else {
    cout<<"\nMatch Not Found";
    }
}
```

**Output**
Enter Text: Sample Text
Enter Pattern: ple
Match Found At: 3

## 15.4.3 Knuth-Morris-Pratt Algorithm (KMP)

This algorithm is best suitable when the pattern is in the redundant characters. This algorithm reduces the duplicate comparisons in the inner loop of the process. If the B-M Algorithm discovers a pattern character that does not match in the text, then the algorithm throws the matched information or knowledge away. KMP Algorithm uses those matched or knowledge about the pattern to avoid unnecessary checks.

This algorithm works with a *failure function*. This failure function is used to find the exact shift of P. So, the algorithm can reuse the previous performed comparisons.

### Failure function

The failure function f(j) can be defined as the length of the longest prefix of P that occurs as a suffix of P[1..j]. The failure function starts by assigning f(0)=0. The failure function calculates the exact shift location of P.

### KMP ALGORITHM

```
/*
T is a Text string
P is a pattern string.
*/
```

### ALGORITHM 15.3: KMP(T[1 .. n], P[1 ..m])

```
j=1
for i=1 to n
while j>0 and T[i]≠P[j] do
j=fail[j]
if j=m //Pattern Found
return (i-m+1)
else
j <- j+1
return 'There is no substring of T matching P.'
```

### FAILURE_FUNCTION(P[1 .. m])

```
j <- 0
f(0) <- 0
for i=1 to m
if P[i]=P[j]
f[i] <- j
else
fail[i] <- j
while j>0 and P[i]≠P[j]
j=fail[j]
j <- j+1
```

In the KMP matching algorithm, at the same time the “i” and “j” are incremented, or “j” is decremented and the value of “i” is kept unchanged.

## Program 15.3

```cpp
// Knuth-Morris-Pratt
//include<iostream.h
#include<string.h>
#include<conio.h>
int n,m, fail[256] ;
char T[512], P[256] ;
void FailureFunction()
{
int i,j;
fail[0]=0;
m=strlen(P); //Length of Pattern String
j=0;
i=1;
while(i<m)
{
if(P[j]==P[i])
{
fail[i]=j+1;
i++;
j++;
}
else
if(j>0)j=fail[j-1];
else
{
fail[i]=0;
i++;
}
}
}
void main()
{
char ch;
int i,j,flag=0;
clrscr();

//Reading of Text
cout<<"\nEnter Text (At End press dot(.)):";
i=0;
while((ch=getche())!='.')
{
T[i]=ch;
i++;
}
T[i]='\0';
cout<<"\nText:" << T;

//Reading of Pattern
cout<<"\nEnter Pattern (At End press dot(.)):";
i=0;
while((ch=getche())!='.')
{
P[i]=ch;
i++;
}
P[i]='\0';
cout<<"\nPattern:" << P;

n=strlen(T);
m=strlen(P);
FailureFunction();
i=j=0;
while(i<n)
{
    if(P[j]==T[i])
    {
        if(j==(m-1))
        {
            cout<<"\nPattern Found AT: "<<(i-m+1);
            flag=1;
        }
        i++;
        j++;
    }
    else if(j!=0) j=fail[j-1];
    else i++;
}
if(flag==0)
{
    cout<<"\nPattern Not Found";
}
```

### Output

Enter Text (At End press dot(.)):ababacab.
Text:
ababacab
Enter Pattern (At End press dot(.)):abacab.
Pattern:
abacab
Pattern Found AT:2

The above-discussed algorithms are best suitable for comparing the single time pattern search over a short length of text string.

## 15.5 APPLICATIONS OF PATTERN MATCHING ALGORITHMS

Various applications of pattern matching algorithms are discussed below.

- **Search engines:** Most efficient pattern matching algorithms are needed for the information retrieval from the internet. A search engine examines all the domains, extracts the Web pages from the Web sites and prepares possible patterns (indexes) that the users of the search engine expect.

For example, if the pattern "pattern matching algorithms" is to be searched, the search engines have to give the reply within seconds. But, the whole Web data will be in millions of tera bytes. Searching for the given pattern on bulk data within the short span of time is really a challenging thing. The search engine service providers do the offline processing for finding the possible sequence of patterns and keep the index terms for the possible Web pages. For searching the index words or patterns from the bulk data, the search engine service providers need highly sophisticated pattern matching algorithms. The pattern matching algorithms are also needed for providing the relevant answers to the search queries.

- **Database management systems:** The database management systems contain data and the interface for the data such as query language interfaces. If any query has to be processed on the data, the DBMS should have an efficient pattern matching algorithm. Because database systems organize bulk of data, the query processing system of the database management system should have an efficient pattern matching algorithm.

- **Signature-based intrusion detection systems:** Intrusion Detection Systems (IDS) are the systems that provide security for the corporate network. Most of the IDS work with signature logic. Here signatures are nothing but the attack patterns. The IDS maintain a large number of signatures to detect various kinds of attacks. If any packet arrives to the IDS, the system has to cross check with available signatures. If any signature matches against the arrived packet, then the IDS alerts the administrator. For cross checking the signatures (attack patterns) against the arrived packet, pattern matching algorithms are required.

- **Text editors:** The text editors like notepad provide facilities like adding text, modifying text, deleting the text and an interface for searching patterns on the text file to the users. For searching text (pattern) on the text file, the pattern matching algorithms are required.

## 15.6 TRIES

A trie pronounced as 'try' is a tree-based data structure, stores the large text string as a tree for fast pattern matching. The word "trie" came from the word "retrieval". When multiple patterns are to be searched over a large text string, the tries are best suitable.

Unlike binary trees, the tries can have any number of children. The pattern matching starts by matching the prefix of the text string to be compared. Trie is a tree-like structure, the shape of the trie depends on the data nodes that the trie holds.

**Different types of tries:**

- Standard Tries
- Compressed Tries
- Suffix Tries

### 15.6.1 STANDARD TRIES

In the standard tries, each character is represented as a node in the tree. Standard trie starts with a node called root node. If a set of strings (say 'S') is to be processed for the pattern matching with multiple patterns, then the standard trie preprocesses (stores the strings) as a tree. If all the sets of strings of 'S' do not have the different prefix characters, then the tree becomes an ordered tree.

This approach avoids the multitime character matching. The procedure returns the index occurrences of the pattern by a single time match. It uses less storage space and a fast pattern search. Standard tries are suitable for the application like search for a word in a document.

Let a set of strings S = {ant, animal, blew, blue} is to be searched for the specified pattern, in the preprocessing step the set 'S' is arranged as a tree as shown in Figure 15.3.
