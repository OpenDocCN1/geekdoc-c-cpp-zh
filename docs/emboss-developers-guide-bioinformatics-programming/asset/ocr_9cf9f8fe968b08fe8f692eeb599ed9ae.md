```
/* Convert single letter to three letter amino acid code. */
AJBool ajResidueToTriplet (char c, AjPStr *Paa3);

/* Convert three letter to single letter amino acid code. */
AJBool ajResidueFromTriplet (char *aa4, char *Pc);
```

# 6.7.17 DNA calculations

Various functions for calculating the properties of nucleotide sequences are provided in ajdan.h/c. These functions use a DNA melting object (AjPMelt) but this is transparent to the application programmer, you will never need to instantiate or use the object directly:

AjPMelt Used for DNA melting

# 6.7.17.1 General functions for DNA melting

The AjPMeltInit and AjPMeltExit functions are used internally to initialise and clean up memory. There is no need to call them directly. The AjPMeltGC function is a utility to calculate G+C content:

```
/* Initialises melt entropies, enthalpies and energies. Different data files are
read for DNA or RNA heteroduplex. Also sets optional flag for array saving of the
above. */
void ajMeltInit (AJBool isdna, ajint savesize);

/* Cleans up DNA melting processing internal memory */
void ajMeltExit (void);

/* Calculates GC fraction of a sequence allowing for ambiguity */
float ajMeltGC (const AjPStr strand, ajint len);
```

# 6.7.17.2 Calculating DNA melting and annealing temperatures and energies

AjPMeltEnergy calculates melt energy and enthalpy/entropy for a sequence string. AjPMeltEnergy2 is an alternative interface that initialises a set of 'save' arrays to make later calls more efficient by inspecting the sequence only once. AjPMeltTemp calculates a melting temperature for an oligonucleotide, with a AjPMeltTempSave version that uses 'save' arrays for efficiency. AjPMeltTempProd calculated the melting temperature of an oligonucleotide product under a given salt concentration. AjPMeltTemp calcualtes the annealing temperature of a product and primer, given their respective melting temperatures.

```
/* Calculate melt energy and enthalpy/entropy for a sequence */
float ajMeltEnergy(const AjPStr strand, ajint len,
                ajint shift, AJBool isDNA,
                AJBool maySave, float *enthalpy, float *entropy);

/* Calculate melt energy for programs like prima */
float ajMeltEnergy2(const char *strand, ajint pos, ajint len,
```