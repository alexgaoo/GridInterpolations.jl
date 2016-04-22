# GridInterpolations

[![Build Status](https://travis-ci.org/sisl/GridInterpolations.jl.svg?branch=master)](https://travis-ci.org/sisl/GridInterpolations.jl)
[![Coverage Status](https://coveralls.io/repos/sisl/GridInterpolations.jl/badge.svg)](https://coveralls.io/r/sisl/GridInterpolations.jl)

This package performs multivariate interpolation on a rectilinear grid. At the moment, it provides implementations of multilinear, simplex, and nearest neighbor interpolation.

For a description of multilinear and simplex interpolation see: Scott Davies, _Multidimensional Triangulation and Interpolation for Reinforcement Learning_, Advances in Neural Information Processing Systems, Cambridge, MA: MIT Press, 1997. [pdf](http://papers.nips.cc/paper/1229-multidimensional-triangulation-and-interpolation-for-reinforcement-learning.pdf)

There are some related packages, such as [Grid.jl](https://github.com/timholy/Grid.jl) and [Interpolations.jl](https://github.com/tlycken/Interpolations.jl).

## Installation

Start Julia and run the following command:

```julia
Pkg.add("GridInterpolations")
```

## Usage

To use the GridInterpolations module, begin your code with

```julia
using GridInterpolations
```

## Interpolation

Create two-dimensional rectangular and simplex interpolation grids, a data array, and a point of interest:
```julia
grid = RectangleGrid([0., 0.5, 1.],[0., 0.5, 1.])  	# rectangular grid
sGrid = SimplexGrid([0., 0.5, 1.],[0., 0.5, 1.])	# simplex grid
nGrid = NearestGrid([0., 0.5, 1.],[0., 0.5, 1.])   	# nearest neighbor grid 
gridData = [8., 1., 6., 3., 5., 7., 4., 9., 2.]   	# vector of value data at each cut
x = [0.25, 0.75]  									# point at which to perform interpolation
```

Perform interpolation on the rectangular grid:
```julia
julia> interpolate(grid,gridData,x)
5.25
```

Or interpolate on the simplex grid:
```julia
julia> interpolate(sGrid,gridData,x)
6.0
```

Or interpolate on the nearest neighbor grid:
```julia
julia> interpolate(nGrid,gridData,x)
1.0 
```

Compute interpolants for the rectangular, simplex, and nearest neighbor grids:
```julia
julia> sGrid = SimplexGrid([0., 0.5, 1.],[0., 0.5, 1.])
[[0.0,0.5,1.0],[0.0,0.5,1.0]]

julia> interpolants(sGrid, x)
([4,5,8],[0.5,0.0,0.5])
```

Convert an index to a Grid coordinate:
```julia
julia> ind2x(grid, 3)
2-element Array{Float64,1}:
 1.0
 0.0
```

Number of verticies in the grid:
```julia
julia> length(grid)
9
```

Number of dimensions:
```julia
julia> dimensions(grid)
2
```

## Credits

Contributors to this package include Maxim Egorov, Eric Mueller, Alex Gao, and Mykel Kochenderfer.
