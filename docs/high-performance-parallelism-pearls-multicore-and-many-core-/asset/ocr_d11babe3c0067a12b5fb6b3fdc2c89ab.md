(1) Download the NAS Parallel Benchmarks (reference at the end of this chapter). I found these directions a little cryptic and misleading.
a. Click on the "NAS software download site" link. You’ll find it underneath the "Summary of source code releases" table.
b. Click on the "Software Request Form". Though the implication is that you need to submit a form and will likely hear back from some official agency in a few days, it is actually a click through download wizard.
c. Select "NPB- NAS Parallel Benchmarks" and then "Next".
d. The rest of the processes are bureaucratic and excessive, but eventually you’ll be able to download the version you want. We will assume you downloaded NPB3.3.1.tar for our instructions.

(2) Untar. Note that you may find that even though the file is labeled tar.gz, it is in fact just a tar file

```
tar xfv NPB3.3.1.tar
```

(3) Use the OpenMP version

```
cd NPB3.3.1/NPB3.3-OMP/
```

(4) Use the make.def_intel template under config/NAS.samples

```
cd config
cp NAS.samples/make.def_intel ./make.def
```

# BUILD FOR THE INTEL® XEON® PROCESSOR

(5) Build the EP benchmark for the Intel Xeon processor. The binary is in NPB3.3.1/NPB3.3-OMP/bin and is called ep.C. Rename it to ep.C.x to distinguish it from the coprocessor version.

```
# From the directory NPB3.3.1/NPB3.3-OMP/
make EP CLASS=C VERSION=VEC
mv bin/ep.C bin/ep.C.x
```

# BUILD FOR THE INTEL XEON PHI COPROCESSOR

(6) Modify the make.def to cross compile for the Intel Xeon Phi coprocessor by modifying the following lines within make.def

```
FFLAGS = -O3 -openmp -mmic
FLINKFLAGS = -O3 -openmp -mmic
CFLAGS = -O3 -openmp -mmic
CLINKFLAGS = -O3 -openmp -mmic
```

(7) Build the EP benchmark for the Intel Xeon Phi coprocessor. The binary is in NPB3.3.1/NPB3.3-OMP/bin and is called ep.C. Rename it to ep.C.knc to distinguish it from the processor version.

```
# From the directory NPB3.3.1/NPB3.3-OMP/
make EP CLASS=C VERSION=VEC
mv bin/ep.C bin/ep.C.knc
```

# FIGURE 25.1

Building the NAS Parallel Benchmark EP for a Class C problem size for both the Intel Xeon processor and the Intel Xeon Phi coprocessor.