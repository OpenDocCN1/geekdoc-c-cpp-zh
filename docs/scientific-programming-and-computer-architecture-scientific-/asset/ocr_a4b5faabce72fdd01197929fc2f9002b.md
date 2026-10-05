Open MPI library is willing to generate RDMA requests during MPI_Testany().^{12}
The definition of the member function transpose(), which is the heart of the
class FastTrans, follows:

```
void FastTrans::transpose(double *localMN,
                    double *localNM){
    for(int q=0; q < P; q++){
        int nrcvd = 0;
        for(int i=0; i < P; i++){
            int q = sendbuf[i];
            copyUSend(q, localMN);
            postend(q);
            int flag;
            MPI_Testany(P, reqlist, &q, &flag,
                        MPI_STATUS_IGNORE);
            if(flag != 0){
                rcvd_list[nrcvd] = q;
                nrcvd++;
            }
        }
    int ncpyd = 0;
    while(nrcvd < P){
        if(ncpyd < nrcvd){
            int q = rcvd_list[ncpyd];
            copyFromrecvbuf(q, localNM);
            ncpyd++;
        }
        int q;
        int flag;
        MPI_Testany(P, reqlist, &q, &flag,);
```

> 12}In view of the considerable investment in Infiniband and Infiniband-like technologies, it is unfortunate that it is so difficult to find out when MPI send/receive result in RDMA transfers, with the answer being implementation dependent.