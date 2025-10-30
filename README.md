# Cara

An isomorphism-aware #SAT solver

**Supported OS**: Linux, macOS (Intel and Apple Silicon), Windows

> [!NOTE]
> A knowledge compiler that uses the same core to compile CNF formulae into wDNNF, pwDNNF, nwDNNF and (smooth) decision-DNNF circuits can be found <a href="https://github.com/Illner/BellaCompiler" target="_blank">here</a>.

## 🏆 Competition Results

In its debut at the **<a href="https://mccompetition.org/assets/files/2025/mccomp_results_25.pdf" target="_blank">Model Counting Competition 2025</a> (MCC 2025)**, Cara achieved:

* **2nd Place** (Track 1, Exact Model Counting)
* **Best Newcomer Award**

To the best of our knowledge, Cara is the **first isomorphism-aware #SAT solver** to ever participate in the MCC. Significantly, these results were achieved with isomorphism-aware caching enabled. This demonstrates Cara's high competitiveness despite
the inherent overhead of this technique, which can be time-consuming on non-symmetric or less symmetric instances.

## Running Cara

To run the #SAT solver:

```console
./Cara -h
```

```console
./Cara < -ph | -ka | -cd > -i input_file -nsm integer (min: 0, max: 10) 
       [ -mmbf positive_integer (default: 1) ] [ -n | -ndc | -nsc ]
```

> [!TIP]
> On Windows, hMETIS is significantly slower because it communicates via files.
> Therefore, we suggest using KaHyPar instead.

### Configurations

Partitioning hypergraph types: <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-ph** — PaToH (Linux, macOS), hMETIS (Windows) <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-ka** — KaHyPar (Linux, macOS, Windows) <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-cd** — Cara (Linux, macOS)

Files: <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-i** — specifies the CNF file name

Preprocessing types of Cara caching scheme: <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-n** — none *(default)* <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-ndc** — removes duplicate clauses <br>
&nbsp;&nbsp;&nbsp;&nbsp; **-nsc** — removes clauses subsumed by others

**-nsm** — sets the number of sample moments *(min: 0, max: 10)* <br>
**-mmbf** — multiplies the model count by this factor (for example, <a href="https://github.com/meelgroup/arjun" target="_blank">Arjun's</a> "MUST MULTIPLY BY" factor) *(default: 1)*

### Syntax of output

The output follows the format defined by <a href="https://mccompetition.org/assets/files/mccomp_format_24.pdf" target="_blank">the model counting competition</a>.

## HydraTest

```console
./HydraTest
```

> [!WARNING]
> Some tests for caching assume that the type "unsigned long long int" has precisely 64 bits.

> [!NOTE]
> The test takes around 10 seconds.

## CaraTest

```console
./CaraTest
```

> [!NOTE]
> The test takes around 10 minutes.

## Used software

### SAT solver

* <a href="https://github.com/crillab/d4v2" target="_blank"> MiniSat 2.2.0 (d4 version) </a>
* <a href="https://github.com/niklasso/minisat" target="_blank"> MiniSat 2.2.0 </a> (<i>implemented, not used</i>)
* <a href="https://github.com/arminbiere/cadical" target="_blank"> CaDiCaL 2.1.3 </a> (<i>TBD</i>)

### Hash map

* <a href="https://github.com/martinus/unordered_dense" target="_blank"> unordered_dense v4.5.0 </a>
* <a href="https://github.com/martinus/robin-hood-hashing" target="_blank"> robin-hood-hashing 3.11.5 </a>
* <a href="https://github.com/skarupke/flat_hash_map" target="_blank"> flat_hash_map </a> (<i>implemented, not used</i>)

### Hypergraph partitioning

* <a href="https://faculty.cc.gatech.edu/~umit/software.html" target="_blank"> PaToH v3.3 </a> (<i>used for Linux, and macOS</i>)
* <a href="http://glaros.dtc.umn.edu/gkhome/metis/hmetis/overview" target="_blank"> hMETIS 1.5 </a> (<i>used only for Windows</i>)
* <a href="https://kahypar.org/" target="_blank"> KaHyPar v.1.3.3 </a>

### Other

* <a href="https://www.boost.org/" target="_blank"> Boost </a>

## Papers

If you use **Cara** in an academic setting, please cite the following paper, which describes the caching scheme on which Cara is based:

    @article{Illner_2025, 
        author  = {Illner, Petr}, 
        title   = {New Compilation Languages Based on Restricted Weak Decomposability}, 
        volume  = {39}, 
        url     = {https://ojs.aaai.org/index.php/AAAI/article/view/33643}, 
        DOI     = {10.1609/aaai.v39i14.33643}, 
        number  = {14}, 
        journal = {Proceedings of the AAAI Conference on Artificial Intelligence}, 
        year    = {2025}, 
        month   = {Apr.}, 
        pages   = {14987-14996} 
    }
