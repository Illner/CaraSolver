# Cara

An isomorphism-aware #SAT solver.

**Supported OS**: Linux, macOS (Apple Silicon), and Windows

> [!IMPORTANT]
> The source code is available in the [Hydra repository](https://github.com/Illner/Hydra).

> [!NOTE]
> **Bella**, a knowledge compiler for wDNNF, pwDNNF, nwDNNF, and (s)d-DNNF circuits using the same core, is available in the [BellaCompiler repository](https://github.com/Illner/BellaCompiler).

## 🏆 Competition Results

In its debut at the **[Model Counting Competition 2025](https://mccompetition.org/assets/files/2025/MC2025_awards.pdf) (MCC-25)**, Cara achieved:

* **2nd Place** (Track 1, Exact Model Counting)
* **Best Newcomer Award**

To the best of our knowledge, Cara is the **first isomorphism-aware #SAT solver** ever to participate in the MCC. Significantly, these results were achieved with isomorphism-aware caching enabled. This demonstrates that Cara remains competitive despite the overhead of this technique, which can be time-consuming on non-symmetric or less symmetric instances.

## Running Cara

To print the help:

```console
./Cara -h
```

To print the version:

```console
./Cara -v
```

To run the #SAT solver:

```console
./Cara < -ph | -ka | -cd > -i input_file -nsm integer (min: 0, max: 10)
       [ -mmbf positive_integer (default: 1) ] [ -n | -ndc | -nsc ]
```

### Recommended Usage

On Linux and macOS:

```console
./Cara -ph -nsm 3 -i input_file
```

On Windows:

```console
./Cara -ka -nsm 3 -i input_file
```

> [!TIP]
> On Windows, hMETIS is significantly slower because it communicates via files.
> Therefore, we suggest using KaHyPar instead.

### Configurations

Hypergraph partitioning:
* **-ph** — PaToH (Linux and macOS), hMETIS (Windows) *(**recommended** on Linux and macOS)*
* **-ka** — KaHyPar (Linux, macOS, and Windows) *(**recommended** on Windows)*
* **-cd** — Cara (Linux and macOS) *(MCC-25 submission configuration)*

Files:
* **-i** — specify the CNF file name

Preprocessing types of Cara caching scheme:
* **-n** — none *(default)*
* **-ndc** — remove duplicate clauses
* **-nsc** — remove clauses subsumed by others

Other options:
* **-h** — print the help message
* **-v** — print version information
* **-nsm** — set the number of sample moments *(min: 0, max: 10)*
* **-mmbf** — multiply the model count by this factor (for example, when using a preprocessor such as [Arjun](https://github.com/meelgroup/arjun) that reports a multiplier) *(default: 1)*

### Syntax of Output

The output follows the format defined by [the model counting competition](https://mccompetition.org/assets/files/mccomp_format_24.pdf).

## Tests

Cara ships with two test binaries. Run both to verify a build.

### HydraTest

```console
./HydraTest
```

> [!WARNING]
> Some tests for caching assume that the type `unsigned long long int` has precisely 64 bits.

> [!NOTE]
> The test takes around 10 seconds.

### CaraTest

```console
./CaraTest
```

> [!NOTE]
> The test takes around 10 minutes.

## Third-Party Software

### SAT Solvers

* [MiniSat 2.2.0 (d4v2 version)](https://github.com/crillab/d4v2)

* [Glucose 3.0 (d4v2 version)](https://github.com/crillab/d4v2) — _work in progress_

* [MiniSat 2.2.0](https://github.com/niklasso/minisat) — _implemented, not used_

* [CaDiCaL 3.0.0](https://github.com/arminbiere/cadical) — _work in progress_

### Hash Maps

* [unordered_dense v4.5.0](https://github.com/martinus/unordered_dense)

* [robin-hood-hashing 3.11.5](https://github.com/martinus/robin-hood-hashing)

* [flat_hash_map](https://github.com/skarupke/flat_hash_map) — _implemented, not used_

### Hypergraph Partitioning

* [PaToH v3.3](https://faculty.cc.gatech.edu/~umit/software.html) — _used on Linux and macOS_

* [hMETIS 1.5.3](https://papers.karypis.org/glaros/software/metis/overview.html) — _used only on Windows_

* [KaHyPar v.1.3.3](https://kahypar.org/) — _used on Linux, macOS, and Windows_

## Licence

Cara is released under the [MIT License](LICENSE). The bundled third-party software components (see above) are subject to their own licences. Some of them are restricted to academic and research use. For the licences, see `Hydra/external/` in
the [Hydra repository](https://github.com/Illner/Hydra).

## Papers

If you use **Cara** in an academic setting, please cite the following paper, which describes the caching scheme on which Cara is based:

```bibtex
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
```
