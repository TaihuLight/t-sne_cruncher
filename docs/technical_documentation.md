# Crunch.py technical documentation

## About

### Project structure

The entry point is [`crunch.py`](../crunch.py) in the project root folder.

The [subprocesses](../subprocesses) folder contains the main processing functions related to data loading, feature extraction and dimensionality reduction.

The [utils](../utils) folder contains miscellaneous functions and data structures that are used elsewhere.

The test folder contains all unit and integration tests. The interal structure of the folder mirrors that of the project itself. I.e. tests for subprocesses are in [`test/subprocesses`](../test/subprocesses) and tests for [`crunch.py`](../crunch.py) are in the [`test/`](../test) root.

### Feature extraction

All feature extraction functions are in [fingerprint.py](../subprocesses/fingerprint.py). The extractions themselves are done using functions in the librosa library.

Extraction is done by mapping input files to fingerprints using a processing pool. As such the process is fairy good at utilizing available processing power and has a fairly sane memory footprint.

### Dimensionality reduction

The two available dimensionality reduction algorithms are t-SNE and PCA. Both are called from the scikit-learn python libraries.

t-SNE can be run with multiple perplexities either in parallel or series. The memory footprint for the algorithms is fairly large so large scale parallelization is discouraged unless loads of memory is available. The t-SNE implementation in scikit is not that well parallelizable so running reductions in series will not efficiently utilize processing power available.

PCA is mostly useful for getting a reductions for data sets that are too large for t-SNE's memory consumption.

### Coloration

Tag based coloration is generated by:

* Calculating the center of gravity for tags. 
* Creating a minimum spanning tree of the center of gravity coordinates.
* Assigning as distant as possible colors to nodes close to each other in the spanning tree.

Color generation is done by creating [hsv](https://en.wikipedia.org/wiki/HSL_and_HSV) colors by setting saturation and value to full and letting the number of tag values determine the step between colors in hue. The colors are then converted to six digit  [html hex](https://en.wikipedia.org/wiki/Web_colors#Hex_triplet) rgb values.

Note that due to the limited resolution of web colors only 1528 colors can be genereted in the described way. Due to this, if tags have more than 1528 different values, a randomish assignment will be used instead. Close neighbours should still have very distinct colors but coloration may be bad in a neighbourhood.

## Testing

Unit and integration testing is automated. 

Tests are written with PyUnit.

Tests can be run locally from the project root with `python3.6 -m unittest discover`. Coverage can be collected with `coverage run -m unittest`, provided the coverage package is installed.

If using [pycharm](www.jetbrains.com/PyCharm) tests and coverage can be run using a *python test* configuration with "Target Path": *project_root/test* and "Working directory": *project_root*.

On pushing changes to [github](https://github.com/SSGL-SEP/t-sne_cruncher), [TravisCI](https://travis-ci.org/SSGL-SEP/t-sne_cruncher) automatically runs unit tests and [codeclimate](https://codeclimate.com/github/SSGL-SEP/t-sne_cruncher) does static analysis on the code.
