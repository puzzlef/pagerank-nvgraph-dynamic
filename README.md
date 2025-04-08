Comparision of **Dynamic** *nvGraph PageRank* with Static approach.

<br>


### Comparision with Static approach

This experiment ([compare-static]) was for comparing the performance between finding **static**
[nvGraph] pagerank of updated graph, and finding **dynamic** [nvGraph] pagerank,
**scaling** old vertices, and using **1/N** for new vertices. Both techniques
were attempted on a number of temporal graphs, running each with multiple batch
sizes (`1`, `5`, `10`, `50`, ...). New edges are incrementally added to the
graph batch-by-batch until the entire graph is complete. **Dynamic pagerank** is
clearly **faster** than *static pagerank* for most cases.

[![](https://i.imgur.com/VOy7mNK.gif)][sheets]
[![](https://i.imgur.com/AB8sxAp.gif)][sheets]
[![](https://i.imgur.com/0N6Qlyb.gif)][sheets]
[![](https://i.imgur.com/ANicp4t.gif)][sheets]
[![](https://i.imgur.com/uKb0yfa.gif)][sheets]
[![](https://i.imgur.com/xuyBgcC.gif)][sheets]
[![](https://i.imgur.com/1hWPVEr.gif)][sheets]

[compare-static]: https://github.com/puzzlef/pagerank-nvgraph-dynamic/tree/compare-static

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
![](https://ga-beacon.deno.dev/G-KD28SG54JQ:hbAybl6nQFOtmVxW4if3xw/github.com/puzzlef/pagerank-nvgraph-dynamic)

[Prof. Dip Sankar Banerjee]: https://sites.google.com/site/dipsankarban/
[Prof. Kishore Kothapalli]: https://cstar.iiit.ac.in/~kkishore/
[Stanford Large Network Dataset Collection]: http://snap.stanford.edu/data/index.html
[nvGraph]: https://github.com/rapidsai/nvgraph
[scaled-fill]: https://github.com/puzzlef/pagerank-dynamic
[charts]: https://photos.app.goo.gl/hYkWA66CWaKkEhs8A
[sheets]: https://docs.google.com/spreadsheets/d/132ja_3B6c33BYcrf38Z7YV4sZOf5AT2Q_md5Y2znX3c/edit?usp=sharing
