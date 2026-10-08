```
************************************************************************/
/* functoctotcost: Compute the Total Cost of All Cars of All Models */
/* in All Stores                                                    */
/*                                                    */
************************************************************************/
/* Input Parameters:                                                   */
/* totstorecost1[ ] - cost of cars in each store                */
/* Returned Variables:                                                  */
/* totcostventl - total cost of all cars in inventory          */
************************************************************************/
float functoctotcost(float totstorecost1[])
{
    int i;
    float totcostinventl = 0;
    for(i = 0; i < IMAX; i++)
        totcostinventl += totstorecost1[i];
    return totcostinventl;
}
************************************************************************/
/* funcoutput: Output of the Cars of Each Model in Each Store      */
/* Total Cars in Each Store and Each Model,                        */
/* Total Number of Cars in All Stores and                           */
/* Total Number of Cars of All Models, and Overall               */
/* Value of All Cars                                                */
************************************************************************/
/* Input Parameters:                                                   */
/* carunits1[ ]][IMAX] - number of cars in each store and model     */
/* totcostcars1[ ]][IMAX] - cost of cars of each store and       */
/* in all models                                                  */
/* totstorecars1[ ] - number of cars in each store                */
/* totmodelcars1[ ] - number of cars of each model                */
/* totstorecost1[ ] - cost of all cars in each store             */
/* totmodelcost1[ ] - cost of cars of each model                  */
```