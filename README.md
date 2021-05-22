Performance of [nvGraph] based static vs dynamic PageRank ([scaled-fill]).

This experiment was for comparing the performance between:
1. Find static pagerank of updated graph.
2. Find dynamic pagerank, **scaling** old vertices, and using **1/N** for new vertices.

Both techniques were attempted on different temporal graphs, updating each
graph with multiple batch sizes. Batch sizes are always an order of 10. New
edges are incrementally added to the graph batch-by-batch until the entire
graph is complete. For some reason, there is only a small speedup of dynamic
pagerank compared to static when batch size is **1000**. Could this be because
of some optimization in nvGraph which makes it fast if initials ranks is not
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
# order: 986 size: 24928 {}
#
# # Batch size 1e+0
# [00003.239 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00000.245 ms; 000 iters.] [3.9897e-7 err.] pagerankDynamic
#
# # Batch size 5e+0
# [00003.273 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00000.564 ms; 000 iters.] [6.9432e-7 err.] pagerankDynamic
#
# # Batch size 1e+1
# [00003.257 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00000.730 ms; 000 iters.] [7.9544e-7 err.] pagerankDynamic
#
# # Batch size 5e+1
# [00003.262 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00001.377 ms; 000 iters.] [1.2863e-6 err.] pagerankDynamic
#
# # Batch size 1e+2
# [00003.256 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00001.627 ms; 000 iters.] [1.3745e-6 err.] pagerankDynamic
#
# # Batch size 5e+2
# [00003.257 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00002.045 ms; 000 iters.] [1.3960e-6 err.] pagerankDynamic
#
# # Batch size 1e+3
# [00003.259 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00002.225 ms; 000 iters.] [1.3943e-6 err.] pagerankDynamic
```

<br>

```bash
$ nvcc -std=c++17 -Xcompiler -lnvgraph -O3 main.cxx
$ ./a.out ~/data/wiki-talk-temporal.txt

# (SHORTENED)
# Using graph wiki-talk-temporal.txt ...
# Temporal edges: 7833141
# order: 1140122 size: 3309560 {}
#
# # Batch size 1e+0
# [00008.260 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00000.565 ms; 000 iters.] [1.0202e-6 err.] pagerankDynamic
#
# # Batch size 5e+0
# [00008.251 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00001.387 ms; 000 iters.] [1.8660e-6 err.] pagerankDynamic
#
# # Batch size 1e+1
# [00008.238 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00001.798 ms; 000 iters.] [2.2741e-6 err.] pagerankDynamic
#
# # Batch size 5e+1
# [00009.137 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00003.628 ms; 000 iters.] [3.0767e-6 err.] pagerankDynamic
#
# # Batch size 1e+2
# [00008.253 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00004.385 ms; 000 iters.] [3.2389e-6 err.] pagerankDynamic
#
# # Batch size 5e+2
# [00009.450 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00007.204 ms; 000 iters.] [3.3589e-6 err.] pagerankDynamic
#
# # Batch size 1e+3
# [00008.152 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00006.344 ms; 000 iters.] [3.3807e-6 err.] pagerankDynamic
#
# # Batch size 5e+3
# [00008.231 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00007.396 ms; 000 iters.] [3.5822e-6 err.] pagerankDynamic
#
# # Batch size 1e+4
# [00010.091 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00008.451 ms; 000 iters.] [3.7259e-6 err.] pagerankDynamic
#
# # Batch size 5e+4
# [00009.121 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00010.248 ms; 000 iters.] [4.2623e-6 err.] pagerankDynamic
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
