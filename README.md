Performance of [nvGraph] based **static** vs **dynamic** PageRank
([scaled-fill]).

This experiment was for comparing the performance between:
1. Find **static** pagerank of updated graph.
2. Find **dynamic** pagerank, **scaling** old vertices, and using **1/N** for new vertices.

Both techniques were attempted on a number of temporal graphs, running each
with multiple batch sizes (`1`, `5`, `10`, `50`, ...). New edges are
incrementally added to the graph batch-by-batch until the entire graph is
complete. **Dynamic pagerank** is clearly **faster** than *static pagerank*
for most cases.

All outputs are saved in [out](out/) and a small part of the output is listed
here. Some [charts] are also included below, generated from [sheets]. The input
data used for this experiment is available at the
[Stanford Large Network Dataset Collection]. This experiment was done with
guidance from [Prof. Dip Sankar Banerjee] and [Prof. Kishore Kothapalli].

<br>

```bash
$ nvcc -std=c++17 -Xcompiler -lnvgraph -O3 main.cu
$ ./a.out ~/data/sx-stackoverflow.txt

# (SHORTENED)
# Using graph sx-stackoverflow.txt ...
# Temporal edges: 63497051
# order: 2601975 size: 36233429 {}
#
# # Batch size 1e+0
# [00051.180 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00003.086 ms; 000 iters.] [1.3436e-6 err.] pagerankDynamic
#
# # Batch size 5e+0
# [00057.530 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00007.709 ms; 000 iters.] [2.2293e-6 err.] pagerankDynamic
#
# # Batch size 1e+1
# [00104.728 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00030.413 ms; 000 iters.] [2.5812e-6 err.] pagerankDynamic
#
# # Batch size 5e+1
# [00103.689 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00051.977 ms; 000 iters.] [3.4487e-6 err.] pagerankDynamic
#
# # Batch size 1e+2
# [00051.169 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00020.250 ms; 000 iters.] [3.6013e-6 err.] pagerankDynamic
#
# # Batch size 5e+2
# [00051.129 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00028.123 ms; 000 iters.] [3.7696e-6 err.] pagerankDynamic
#
# # Batch size 1e+3
# [00051.090 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00030.524 ms; 000 iters.] [3.8050e-6 err.] pagerankDynamic
#
# # Batch size 5e+3
# [00051.178 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00035.398 ms; 000 iters.] [3.8865e-6 err.] pagerankDynamic
#
# # Batch size 1e+4
# [00051.192 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00037.255 ms; 000 iters.] [3.9379e-6 err.] pagerankDynamic
#
# # Batch size 5e+4
# [00051.161 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00041.770 ms; 000 iters.] [4.1385e-6 err.] pagerankDynamic
#
# # Batch size 1e+5
# [00051.124 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00043.506 ms; 000 iters.] [4.2669e-6 err.] pagerankDynamic
#
# # Batch size 5e+5
# [00051.133 ms; 000 iters.] [0.0000e+0 err.] pagerankStatic
# [00047.743 ms; 000 iters.] [4.6767e-6 err.] pagerankDynamic
```

[![](https://i.imgur.com/VOy7mNK.gif)][sheets]
[![](https://i.imgur.com/AB8sxAp.gif)][sheets]
[![](https://i.imgur.com/0N6Qlyb.gif)][sheets]
[![](https://i.imgur.com/ANicp4t.gif)][sheets]
[![](https://i.imgur.com/uKb0yfa.gif)][sheets]
[![](https://i.imgur.com/xuyBgcC.gif)][sheets]
[![](https://i.imgur.com/1hWPVEr.gif)][sheets]

<br>
<br>


## References

- [nvGraph pagerank example, EN605.617, JHU-EP-Intro2GPU](https://github.com/JHU-EP-Intro2GPU/EN605.617/blob/master/module9/nvgraph_examples/nvgraph_Pagerank.cpp)
- [nvGraph pagerank example, CUDA Toolkit Documentation](https://docs.nvidia.com/cuda/archive/10.0/nvgraph/index.html#nvgraph-pagerank-example)
- [nvGraph Library User's Guide](https://docs.nvidia.com/cuda/archive/10.1/pdf/nvGRAPH_Library.pdf)
- [RAPIDS nvGraph NVIDIA graph library][nvGraph]
- [PageRank Algorithm, Mining massive Datasets (CS246), Stanford University](https://www.youtube.com/watch?v=ke9g8hB0MEo)
- [Stanford Large Network Dataset Collection]

<br>
<br>

[![](https://i.imgur.com/N7tUfyV.jpg)](https://www.youtube.com/watch?v=wYps-kGPh78)

[Prof. Dip Sankar Banerjee]: https://sites.google.com/site/dipsankarban/
[Prof. Kishore Kothapalli]: https://cstar.iiit.ac.in/~kkishore/
[Stanford Large Network Dataset Collection]: http://snap.stanford.edu/data/index.html
[nvGraph]: https://github.com/rapidsai/nvgraph
[scaled-fill]: https://github.com/puzzlef/pagerank-dynamic-adjust-ranks
[charts]: https://photos.app.goo.gl/hYkWA66CWaKkEhs8A
[sheets]: https://docs.google.com/spreadsheets/d/132ja_3B6c33BYcrf38Z7YV4sZOf5AT2Q_md5Y2znX3c/edit?usp=sharing
