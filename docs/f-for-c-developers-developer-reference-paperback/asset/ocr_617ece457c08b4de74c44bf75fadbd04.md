let c1 = population.[r()]
let result = if (c0.Fitness(fitnessFunction) > c1.Fitness(fitnessFunction))
then c0
else c1

result.Clone();
Seq.initPopulationSize(fun -> randomSelection())

```
// shuffle crossover
let ShuffleCrossover(c0:ChromosomeType, c1:ChromosomeType) = =
    let crossover c0 = c1
    let isEven n = n%2 = 0
    let randomSwitch(x,y) = if isEven(randomF()) then (x,y) else (y,x)
    List.zip c0 c1 | List.randomSwitch | List.unzip
    let (first,second) = crossover (c0.Genos) (c1.Genos)
c0.Genos < first
c1.Genos < second

// evolve the whole population
let evolve(population:Chromosome list) selectionF crossoverF 
crossoverRate
mutationRate elitism =
    let populationSize = Seq.length length
    let (f) = randomF() % populationSize
    let elites = selectionF population fitnessF | Seq.toList
    let seq0 = elites | Seq.map (fun i element->(i,element)) | Seq.filter (fun
(i,)->i%2<0) | Seq.map (fun (c,b)->b)
    let seq1 = elites | Seq.map (fun i element->(i,element)) | Seq.filter (fun
(i,)->i%2<0) | Seq.map (fun (c,b)->b)
    let crossover(a:ChromosomeType, b:ChromosomeType) = =
        if (randomFloat(F) < crossoverRate) then
            crossover a b
        if (randomFloat(F) < mutationRate) then
            a.Mutate()
        if (randomFloat(F) < mutationRate) then
            b.Mutate()
        [a] @ [b]

    if elitism then
        let seq0 = seq0
        let seq1 = seq1
        let r = Seq.map xoverMutate seq0 seq1 | List.concat
        r.Tail @ [ bestChromosome population fitnessF ]
    else
        Seq.map xoverMutate seq0 seq1 | List.concat

// composite function x times
let rec f x =
    match x with
    | 1 -> f
    | n -> f (x-1))

// convert a function seq to function composition
let composeFunctions functions =
    Seq.fold (>>) id functions
```