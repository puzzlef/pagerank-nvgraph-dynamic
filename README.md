Performance of [nvGraph] based static vs dynamic PageRank ([scaled-fill]).

This experiment was for comparing the performance between:
1. Find static pagerank of updated graph.
2. Find dynamic pagerank, **scaling** old vertices, and using **1/N** for new vertices.

Both techniques were attempted on different temporal graphs, updating each
graph with multiple batch sizes. Batch sizes are always an order of 10. New
edges are incrementally added to the graph batch-by-batch until the entire
graph is complete. For some reason, there is only a minor speedup of dynamic
pagerank compared to static when batch size is **1000**. Could this be because
of some optimization in nvGraph which makes it fast if not initials ranks is
provided, but becomes slow when they are provided?

All outputs (including shortened versions) are saved in [out/](out/) and
outputs for `email-Eu-core-temporal` and `wiki-talk-temporal` are listed here.
The input data used for this experiment is available at ["graphs"] (for small
ones), and the [SuiteSparse Matrix Collection].

<br>

```bash
$ nvcc -std=c++17 -Xcompiler -lnvgraph -O3 main.cxx
$ ./a.out ~/data/email-Eu-core-temporal.txt

# (SHORTENED)
# Using graph email-Eu-core-temporal.txt ...
# Temporal edges: 332335
# order: 986 size: 24929 {}
#
# # Batch size 1e+5
# [00002.473 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00002.303 ms; 000 iters.] [1.0035e-6 err.] pagerankDynamic
#
# # Batch size 1e+4
# [00002.667 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00002.235 ms; 000 iters.] [1.3209e-6 err.] pagerankDynamic
#
# # Batch size 1e+3
# [00002.657 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00001.798 ms; 000 iters.] [1.4059e-6 err.] pagerankDynamic
```

<br>

```bash
$ nvcc -std=c++17 -Xcompiler -lnvgraph -O3 main.cxx
$ ./a.out ~/data/wiki-talk-temporal.txt

# (SHORTENED)
# Using graph wiki-talk-temporal.txt ...
# Temporal edges: 7833141
# order: 1140149 size: 3309592 {}
#
# # Batch size 1e+6
# [00008.820 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00010.340 ms; 000 iters.] [4.3904e-6 err.] pagerankDynamic
#
# # Batch size 1e+5
# [00008.187 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00008.803 ms; 000 iters.] [4.5346e-6 err.] pagerankDynamic
#
# # Batch size 1e+4
# [00008.766 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00008.301 ms; 000 iters.] [3.7298e-6 err.] pagerankDynamic
#
# # Batch size 1e+3
# [00008.154 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00006.408 ms; 000 iters.] [3.3933e-6 err.] pagerankDynamic
```

<br>
<br>


## References

- [nvGraph pagerank example, EN605.617, JHU-EP-Intro2GPU](https://github.com/JHU-EP-Intro2GPU/EN605.617/blob/master/module9/nvgraph_examples/nvgraph_Pagerank.cpp)
- [nvGraph pagerank example, CUDA Toolkit Documentation](https://docs.nvidia.com/cuda/archive/10.0/nvgraph/index.html#nvgraph-pagerank-example)
- [nvGraph Library User's Guide](https://docs.nvidia.com/cuda/archive/10.1/pdf/nvGRAPH_Library.pdf)
- [RAPIDS nvGraph NVIDIA graph library][nvGraph]
- [SuiteSparse Matrix Collection]

<br>
<br>

[![](https://i.imgur.com/sNyLL3K.jpg)](https://www.youtube.com/watch?v=SoiKp2oSUl0)

[nvGraph]: https://github.com/rapidsai/nvgraph
[scaled-fill]: https://github.com/puzzlef/pagerank-dynamic-adjust-ranks
["graphs"]: https://github.com/puzzlef/graphs
[SuiteSparse Matrix Collection]: https://suitesparse-collection-website.herokuapp.com
