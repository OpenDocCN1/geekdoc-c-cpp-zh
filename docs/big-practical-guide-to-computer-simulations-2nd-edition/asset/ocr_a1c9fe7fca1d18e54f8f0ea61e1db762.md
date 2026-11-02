Here, we consider the example of a three dimensional box with atoms, which are going to be represented as spheres. The actual atom data is stored in an array where the elements are of type atom_t which is defined as follows:

GET SOURCE CODE
DIR: literature
FILE(S): atoms.c

```
/* stores data of one atom: */
typedef struct
{
    double      m;      /* mass of atom */
    double      sigma;  /* 'size' of atom for LJ */
    double      epsilon;/* LJ energy parameter */
    double      *x;     /* position of atom */
    double      *v;     /* velocity of atom */
    double      *f;     /* force on atom */
} atom_t;
```

Note that not all data, like the force array f, is necessary for just generating a configuration. Nevertheless, here we state the actual data structure which was used to perform Molecular dynamics simulations, i.e. the integration of Newton's equations of motion. There is also the data structure glas_system_t which holds global information of the model. Here we only need the entries dim, which holds the dimension (here 3) of the system, the entries l[3], l[1], l[2] which store the lateral sizes and N which holds the total number of atoms. The program atoms.c contains a function glas_setup() which takes a pointer to a structure of type glas_system_t, initializes everything, generates a random configuration and returns a pointer to it.

Below, a function is shown which generates a Povray file from the current configuration:

```
void atoms_plot_cfg(atoms_system_t *system, atom_t *atom)
{
    char filename[1000];
    FILE *povfile;
    int t, d;                 /* loop counters */
    double *r;                /* position */

    r = (double *) malloc(system->dim*sizeof(double));
    sprintf(filename, "cfg.pov");   /* open file */
    povfile = fopen(filename, "w");
    fprintf(povfile, "#include \"colors.inc\"\n" /* header etc */
```