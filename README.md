# Density Based Clustering for JavaScript

## Overview

## DBSCAN Clustering for JavaScript

Density-based spatial clustering of applications with noise (DBSCAN) is one of the most popular algorithm for clustering data.
http://en.wikipedia.org/wiki/DBSCAN

## Examples

```
var dataset = [
    [1,1],[0,1],[1,0],
    [10,10],[10,13],[13,13],
    [54,54],[55,55],[89,89],[57,55]
];

var dbscan = new DBSCAN();
var clusters = dbscan.run(dataset, 5, 2);
console.log(clusters, dbscan.noise);

/*
RESULT:
[
    [0,1,2],
    [3,4,5],
    [6,7,9],
    [8]
]

NOISE: [ 8 ]
*/
```

## OPTICS

Ordering points to identify the clustering structure (OPTICS) is an algorithm for clustering data similar to DBSCAN.
The main difference between OPTICS and DBSCAN is that it can handle data of varying densities.
http://en.wikipedia.org/wiki/OPTICS_algorithm

**Important**

Clustering returned by run() function is nearly indistinguishable from a clustering created by DBSCAN.
To extract different density-based clustering as well as hierarchical structure we need to analyse **reachability plot**.
For more information visit http://en.wikipedia.org/wiki/OPTICS_algorithm#Extracting_the_clusters

## Example

```
// REGULAR DENSITY
var dataset = [
    [1,1],[0,1],[1,0],
    [10,10],[10,11],[11,10],
    [50,50],[51,50],[50,51],
    [100,100]
];

var dbscan = new DBSCAN();
var clusters = dbscan.run(dataset, 2, 2);
var plot = optics.getReachabilityPlot();
console.log(clusters, plot);

/*
RESULT:
[
    [0,1,2],
    [3,4,5],
    [6,7,8],
    [9]
]
*/
```

```
// VARYING DENSITY
var dataset = [
    [0,0],[6,0],[-1,0],[0,1],[0,-1],
    [45,45],[45.1,45.2],[45.1,45.3],[45.8,45.5],[45.2,45.3],
    [50,50],[56,50],[50,52],[50,55],[50,51]
];

var dbscan = new DBSCAN();
var clusters = dbscan.run(dataset, 6, 2);
var plot = optics.getReachabilityPlot();
console.log(clusters, plot);

/*
RESULT:
[
    [0, 2, 3, 4],
    [1],
    [5, 6, 7, 9, 8],
    [10, 14, 12, 13],
    [11]
]
*/
```

## Testing

Open folder and run:
```
mocha -R spec
```

## License

Software is licensed under MIT license.
For more information check LICENSE file.