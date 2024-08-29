# signed-heat-3d (3D volumetric domains)

C++ demo for "[A Heat Method for Generalized Signed Distance](https://nzfeng.github.io/research/SignedHeatMethod/index.html)" by [Nicole Feng](https://nzfeng.github.io/index.html) and [Keenan Crane](https://www.cs.cmu.edu/~kmcrane/), presented at SIGGRAPH 2024.

Paper PDF (18.9mb): [link](https://nzfeng.github.io/research/SignedHeatMethod/SignedDistance.pdf)

Project page with links to paper, pseudocode, supplementals, & videos: [link](https://nzfeng.github.io/research/SignedHeatMethod/index.html)

SIGGRAPH talk (10 minutes): [link]()

This Github repository demonstrates the _Signed Heat Method (SHM)_ on **3D volumetric domains**, solving for (generalized) signed distance to triangle meshes, polygon meshes, to point clouds. If you're interested in using the Signed Heat Method in 2D surface domains, go to [this Github repository](https://github.com/nzfeng/signed-heat-demo) which demonstrates the [geometry-central implementation on (2D) surface meshes and point clouds](https://geometry-central.net/surface/algorithms/signed_heat_method/) .

![teaser image](media/teaser.png)

If this code contributes to academic work, please cite as:
```bibtex
@article{Feng:2024:SHM,
    author = {Feng, Nicole and Crane, Keenan},
    title = {A Heat Method for Generalized Signed Distance},
    year = {2024},
    issue_date = {July 2024},
    publisher = {Association for Computing Machinery},
    address = {New York, NY, USA},
    volume = {43},
    number = {4},
    issn = {0730-0301},
    url = {https://doi.org/10.1145/3658220},
    doi = {10.1145/3658220},
    journal = {ACM Trans. Graph.},
    month = {jul},
    articleno = {92},
    numpages = {19}
}
```

## Getting started

This project uses [geometry-central](https://geometry-central.net) for mesh computations, [Tetgen](https://www.wias-berlin.de/software/tetgen/1.5/index.html) for tet mesh generation, [libigl](https://libigl.github.io/) for isosurface extraction, and [Polyscope](http://polyscope.run/) for visualization. These dependencies are added as git submodules, so copies will be downloaded locally when you clone this project as below.

```
git clone --recursive https://github.com/nzfeng/signed-heat-3d.git
cd SHM
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release .. # use `Debug` mode to enable checks
make -j8 # or however many cores you want to use
bin/main /path/to/mesh
```
A Polyscope GUI will open.

# Mesh & point cloud input

## File formats
An input mesh may be an `obj`, `ply`, `off`, or `stl`. See [the geometry-central website](https://geometry-central.net/surface/utilities/io/#reading-meshes) for up-to-date information on supported file types.

An input point cloud should be specified using point positions and normals. Some example files, with extension `.pc`, are in the `data` directory.

# Usage

In addition to the mesh file, you can pass several arguments to the command line, including some flags which are also shown as options in the GUI.

|flag | purpose|
| ------------- |-------------|
|`--g`, `--grid`| Solve on a background grid. By default, the domain will be discretized as a tet mesh. |
|`--V`, `--verbose`| Verbose output. On by default|
|`--h`| Controls the tet/grid spacing, with larger values indicating more refinement. Default value is 1.|
|`--help`| Display help. |

This program lets you solve for distance on either a tet-meshed domain, or a background (uniform) grid. The tetmesh option in particular generates a _conforming_ tetmesh to an input triangle mesh. If your source geometry isn't a triangle mesh (e.g. polygon mesh or point cloud), consider using the grid option.

TODO: Currently no hierarchical summation
TODO: explanation of hCoef

# Output

TODO: isosurfaces