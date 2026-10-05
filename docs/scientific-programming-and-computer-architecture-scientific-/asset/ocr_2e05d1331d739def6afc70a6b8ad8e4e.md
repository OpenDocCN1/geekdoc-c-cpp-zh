# 6.3. MPI examples

```
void FastTrans::FROMrecvbuf(int q,double *localNM){
  long ncols = fstm[p+1]-fstm[p];
  long nrows = fstN[q+1]-fstN[q];
  long rbufindindex = ncols*fstN[q];
  long localindex = fstN[q];
  long lda = N;
  copywlda(recvbuf+rbufindex, nrows, ncols,
localNM+localindex, lda);
}
```

Unlike the corresponding member functions of the class Transpose, these member functions do not use a for-loop to communicate with every other MPI process. As a result, they are slightly more transparent. The functions transpose() and copywlda() are exactly the same as the versions given earlier and are omitted.
The member function postend() and postrec() communicate with a single other process of rank q.

```
void FastTrans::postend(int q){
  long ncols = fstm[p+1]-fstN[p];
  long nrows = fstm[q+1]-fstm[q];
  long sbufindex = ncols*fstm[q];
  int count = ncols*nrows; //MPI can't handle long
  int tag = 0;
  MPI_Isend(sendbuf+sbufindex, count, MPI_DOUBLE,
  q, tag, MPI_COMM_WORLD, sreqlist+q);
```

```
void FastTrans::postrec(int q){
  long ncols = fstm[p+1]-fstm[p];
  long nrows = fstN[q+1]-fstN[q];
  long rbufindindex = ncols*fstN[q];
  int count = nrows*ncols; //MPI can't handle long
  int tag = 0;
  MPI_Irec(recvbuf+rbufindex, count, MPI_DOUBLE,
  q, tag, MPI_COMM_WORLD, rreqlist+q);
```