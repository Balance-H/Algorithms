# CMSA: Efficient Minimal Collapsible Set Construction

## Environment
- **Python Version**: 3.10  
- **Core Implementation**: All performance-critical components are implemented in **C** and compiled into the shared library **`libdecom_h.so`**.  
- **Platform**: Primarily developed and tested on **Linux**.  
- **Source Code**: Available in the Python package **`netdecom`**, which also provides Windows-compatible binaries.

## Notebooks
- **`CMSA_vs_IPA_Performance_Comparison.ipynb`**  
  Performance evaluation of CMSA and IPA on general graphical models.

- **`CMSA_vs_SHAR_Performance_Comparison.ipynb`**  
  Performance evaluation of CMSA and SHAR on decomposable graphical models.

## Chordal Graph Generation
The experiments utilize **SageMath** to generate chordal graphs. Example usage within a SageMath-enabled environment:

```python
from sage.graphs.all import *

# Generate a random chordal graph
g = graphs.RandomChordalGraph(n, algorithm='growing', k=k)

# Parameters:
# n — number of nodes.
# k — parameter controlling the approximate edge density of the generated graph
#     (in general, larger k yields denser graphs).

# By tuning k, users can generate graphs with varying edge densities 
# to benchmark algorithmic performance.

# Note: SageMath must be installed and available in the execution environment 
# for the above function to work.
