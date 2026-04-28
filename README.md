# CMSA: Efficient Minimal Collapsible Set Construction

CMSA is an efficient implementation for constructing minimal collapsible sets in undirected graphical models. The package is designed for large-scale experimental comparison and provides Python-accessible interfaces while keeping all performance-critical routines in C.

## Environment

- **Python Version**: 3.10
- **Core Implementation**: All performance-critical components are implemented in C and compiled into the shared library `libdecom_h.so`.
- **Python Interface**: C functions are exposed to Python through pybind11 bindings written in C++.
- **Platform**: Primarily developed and tested on Linux.
- **Source Code**: Available in the Python package `netdecom`, which also provides Windows-compatible binaries.

## Core Source Files

The low-level implementation is separated into three source files:

| File | Role |
| --- | --- |
| `decom_h.c` | Contains the full C implementation of the core routines and performance-critical algorithms. |
| `decom_h.h` | Declares the C functions, data structures, and interfaces used by the implementation and binding layer. |
| `decom_h.cpp` | Provides the pybind11 binding layer. It wraps the C implementation and exposes the relevant functions as Python-callable interfaces. |

In this design, the algorithmic computation is kept in `decom_h.c`, while `decom_h.cpp` only serves as the C++/pybind11 bridge between the C backend and Python. This keeps the implementation efficient, modular, and easier to maintain.

A typical build process compiles the C and C++ sources together and links them into the shared library:

```bash
decom_h.c  +  decom_h.cpp  +  decom_h.h  -->  libdecom_h.so
```

After compilation, the Python package `netdecom` loads the shared library and provides user-facing Python functions.

## Notebooks

The repository includes two main experimental notebooks:

- **`CMSA_vs_IPA_Performance_Comparison.ipynb`**  
  Performance evaluation of CMSA and IPA on general graphical models.

- **`CMSA_vs_SHAR_Performance_Comparison.ipynb`**  
  Performance evaluation of CMSA and SHAR on decomposable graphical models.

These notebooks are intended to reproduce the main runtime and scalability comparisons reported for CMSA.

## Chordal Graph Generation

Some experiments use **SageMath** to generate random chordal graphs. Example usage in a SageMath-enabled environment:

```python
from sage.graphs.all import *

# Generate a random chordal graph
g = graphs.RandomChordalGraph(n, algorithm='growing', k=k)

# Parameters:
# n — number of nodes.
# k — parameter controlling the approximate edge density of the generated graph.
#     In general, larger k yields denser graphs.
```

By tuning `k`, users can generate graphs with different edge densities and benchmark the performance of CMSA under different graph structures.

> **Note:** SageMath must be installed and available in the execution environment for `graphs.RandomChordalGraph` to work.


## Implementation Notes

- The C backend is responsible for the main graph decomposition and minimal collapsible set construction.
- The C++ file `decom_h.cpp` does not reimplement the algorithm. It only declares and binds the C functions to Python through pybind11.
- The header file `decom_h.h` ensures consistent declarations between the C implementation and the C++ binding layer.
- The compiled shared library `libdecom_h.so` is used on Linux. Windows-compatible binaries are provided through the `netdecom` package.

## Citation

If you use this implementation or the CMSA-related experimental results, please cite:

```text
Heng Pei, He Shiyuan, Sun Yi, and Guo Jianhua.
Revisiting the Results of Madigan and Mosurski on Collapsibility in Contingency Tables.
Biometrika, 2026.
```

A BibTeX entry can be written as:

```bibtex
@article{heng2026revisiting,
  title   = {Revisiting the Results of Madigan and Mosurski on Collapsibility in Contingency Tables},
  author  = {Heng, Pei and He, Shiyuan and Sun, Yi and Guo, Jianhua},
  journal = {Biometrika},
  year    = {2026}
}
```

## License

Please refer to the package or repository license file for licensing information.
