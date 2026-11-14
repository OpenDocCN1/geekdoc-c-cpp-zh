```
fluxer: fluxer.o libmesher.a libsolver.a
${CXX} ${CXXFLAGS} $^ -o $@
```