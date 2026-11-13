that are neighbors, or other cells that are close to each other in the dataset. We can exploit this in the implementation of findCell by caching the previously returned cell and, in subsequent calls, first testing whether the searched location falls in this cell. If so, the function completes without any search. If not, the existing spatial search structure is used.

One limitation of spatial search structures is that they take relatively long to build as compared to the search time. This is not a problem in case of a grid with fixed geometry. If the grid’s geometry changes frequently compared to the number of searches, it can be faster to use a brute-force linear search instead of a spatial search structure.

Unstructured grids. We now turn our attention to unstructured grids. Unstructured grids have the same geometry as structured grids but have a different topology. Yet, we cannot derive a UnstructuredGrid class from StructuredGrid, since the latter also inherits a regular topology from UniformGrid. Hence, we derive UnstructuredGrid directly from the Grid interface as seen in Listing 3.9.

```
class UnstructuredGrid : public Grid
{
    public:
        UnstructuredGrid (int P, int C)
        { points.resize(2*P); cells.resize(3*C); }
    int numCells()
    { return cells.size()/3; }
    int numPoints()
    { return points.size()/2; }
    int getCell(int i, int *c)
    {
        c[0]=cells[3*i]; c[1]=cells[3*i+1];
        c[2]=cells[3*i+2]; return 4;
    }
    void getPoint(int i, float* p)
    { p[0]=points[2*i]; p[1]=points[2*i+1]; }
    void setCell(int i, int* c)
    { cells[3*i]=c[0]; cells[3*i+1]=c[1];
        cells[3*i+2]=c[2]; }
    void setPoint(int i, float* p)
    { points[2*i]=p[0]; points[2*i+1]=p[1]; }
    private:
        vector<int> cells; //Vertex indices for all (triangle) cells
        vector<float> points; //Coordinates for all sample points
};
```

Listing 3.9. Unstructured grid implementation.