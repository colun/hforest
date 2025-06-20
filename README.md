# HilbertForest

HilbertForest is an approximate k-nearest neighbor search library using Hilbert curves.

# SISAP2025 Info BEGIN

## Steps for running

Please refer to the Dockerfile for environment setup instructions.

### Clone this repository

```bash
git clone https://github.com/colun/hforest.git
cd hforest
```

### Run

Build the C++ extension module first:

```bash
make
```

Note: If using the provided Dockerfile, the build step is already completed and you can skip this step.

Then run the tasks on an example input using:

```bash
python sisap2025.py task1
# or
python sisap2025.py task1_shino
# or
python sisap2025.py task2
```

Note on task1 variations:
- `task1`: This is the version tuned by Imamura(colun), which executes with 8 out of 16 hyperparameters optimized for the task1.
- `task1_shino`: This is the version tuned by Shinohara, which executes with the remaining 8 out of 16 hyperparameters optimized for the task1. This version is specifically adjusted to run with zero swap size when launching the Docker container, optimized for low memory usage.

These complementary configurations allow for comprehensive evaluation across different hyperparameter optimization strategies.

The necessary sample datasets will be provided by the contest organizers. 
Please place the files in the `./data` folder with their original filenames as shown in GitHub Actions.

### Evaluation

Evaluation is performed automatically during execution.

# SISAP2025 Info END

# HilbertForest

HilbertForest is an approximate k-nearest neighbor search library using Hilbert curves.

## Features

- Spatial indexing using Hilbert curves
- k-nearest neighbor search support
- Python library with C++ implementation

## Installation

### Requirements

- Python 3.7+
- g++ (C++14 compatible)

### Build

```bash
git clone https://github.com/colun/hforest.git
cd hforest
make
```

## Expected Data Format

This library is optimized for data in one of the following formats:

1. **Unit vectors**: Data normalized to L2 norm of 1
2. **Normalized Gaussian distribution**: Data where each coordinate follows a Gaussian distribution with mean 0 and standard deviation `1/√d` (where d is the number of dimensions)

Performance may degrade for data that significantly deviates from these conditions.

## Main Parameters

### Constructor Parameters

- `db_path` (str, default=""): Directory for index file storage (empty string for in-memory only mode)
- `ntrees` (int, default=10): Number of trees to build (trade-off between accuracy and speed)
- `leaf_size` (int, default=1): Minimum leaf node size
- `verbose` (int, default=1): Verbosity level (0: silent, 1: normal, 2: detailed)
- `seed` (int, default=-1): Random seed (-1 for automatic)

### Search Parameters

After creating the index, you can adjust search behavior with the following parameters:

```python
# Adjust number of trees used during search
index.ntrees = 5            # Use 5 out of the built trees

# Adjust candidate counts
index.odd_candidates = 11   # Number of candidates for leaf nodes with odd size
index.even_candidates = 10  # Number of candidates for leaf nodes with even size
index.dist_candidates = 100 # Number of candidate points for distance calculation

# Search range
index.hops = 1  # Search range around candidate points
```

## Limitations

- Tested with 384-dimensional data
- Index files are stored in the specified directory

## License

This project was developed as an entry for SISAP Challenge 2025.
The official license will be decided after the contest ends.
We are considering a license that welcomes use for academic research and experimental purposes, so please wait a little longer.

Comments and suggestions regarding the license are welcome via [GitHub Issues](https://github.com/colun/hforest/issues).

## Contributing

**Note**: Pull requests are not accepted until the license is decided.
Pull requests created during this period will be closed regardless of content.
Issues with long code snippets may be treated similarly.

Additionally, bug reports and feature requests are not currently being accepted.
After the contest ends and the license is decided, we plan to accept bug reports and feature requests via [GitHub Issues](https://github.com/colun/hforest/issues), so please wait until then.