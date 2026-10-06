# Understanding Concurrent Code Design

```
public:
    CSchwefelP() : CSchwefel() {}
    CSchwefelP(unsigned uSize) : CSchwefel(uSize) { }
    virtual -CSchwefelP(void) { }
    virtual double Evaluate(void* lpParameters = 0);
protected:
    CSchwefelP(const CSchwefel&) {}
    CSchwefelP& operator = (const CSchwefel&) { return *this; }
    virtual TCHAR* ObjectName(void) const { return _T("SchwefelP"); }
private:
    //
};
```

#endif

+   4. Open Solution Explorer and right-click on Source file. Add a new source file named CSchwefelP. Open CSchwefelP.cpp.

```
double CSchwefelP::Evaluate(void* lpParameters)
{
    GetSystemTime(&StartTime());

    double sum = 0;
    double score = 0;
    double min = DBL_MAX;
    double best = DBL_MAX;
    int iSize = (int)iSize();

    #pragma omp parallel firstprivate(min) firstprivate(score)
    {
        #pragma omp for reduction(+: sum) reduction(+: score) nowait
        for (int i = 0; i < iSize; i++)
            sum += Allele(i);

        if (min > Allele(i))
        {
            min = Allele(i);
        }
    }
}
```