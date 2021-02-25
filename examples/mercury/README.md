# Project Mercury

A set of utilities and training scripts around simple and modular large-scale language model training, built by 
Stanford's Project Mercury Team. Instructions on setup, contributing, and extending are below:

## Contributing

As a first step, it's of the utmost importance to maintain code style and general contributing guidelines from the
base `transformers` repository -- please consult [`CONTRIBUTING.md`](../../CONTRIBUTING.md). Please also make sure to
read the [`CODE_OF_CONDUCT`](../../CODE_OF_CONDUCT.md).

This directory was built following the `template` instructions detailed in 
[`templates/adding_a_new_example_script/README.md`](../../templates/adding_a_new_example_script/README.md). Please read
this to get a sense of the starter code and format prescribed by `transformers`.

## Developing

TODO - run `make style` and `make quality` before each commit basically.

## Quickstart 

Working with virtual environments, or some sort of Python dependency manager (Conda, Poetry) with access to `pip` is
a necessary step. Most of the details below are for a `conda` install, but can be mapped to `venv` or `poetry` fairly
easily. If you run into trouble building the Mercury dependencies, please file an Issue!

### GPU & Cluster Environments (Shared)

Clones the Stanford-Mercury fork to the working directory, then walks through dependency setup. NOTE - PyTorch install
is heavily dependent on your current CUDA Toolkit (on available GPUs); make sure you're installing the correct version
as a first step prior to installing the remaining dependencies.

Because this is a shared environment (possibly with a centralized `conda` or other dependency manager) make sure to
name your environment appropriately; crucially, because we're installing `transformers` as an editable Python package,
all your local changes to `transformers` will affect *all* users using the same environment, so it's important to 
shard environments.

```bash
git clone https://github.com/stanford-mercury/transformers.git
cd transformers

# Default branch is not `master`/`main` --> This is to facilitate HF PRs down the line! Default is `mercury-core`
git checkout mercury-core

# Create Conda Environment (or however you like managing dependencies)
conda create --name mercury-<name/branch> python=3.8
conda activate mercury-<name/branch>

# Install PyTorch first -- this will depend on CUDA Kernel so be careful! Stanford GPUs run CUDA = 10.1 (not 11!)
conda install pytorch torchvision torchaudio cudatoolkit=10.1 -c pytorch

# Install `transformers` as an editable source
pip install -e ".[dev]"

# Install `datasets` as an extra source install
git clone https://github.com/huggingface/datasets
cd datasets
pip install -e .
```

### CPU (Usually Local Development)

Similar to the above, but installs the appropriate (CPU-only) versions of PyTorch and `transformers` dependencies.
Because it's local development, you can be less careful about the environments defined.

```bash
git clone https://github.com/stanford-mercury/transformers.git
cd transformers

# Default branch is not `master`/`main` --> This is to facilitate HF PRs down the line! Default is `mercury-core`
git checkout mercury-core

# Create Conda Environment (or however you like managing dependencies)
conda create --name mercury python=3.8
conda activate mercury

# Install PyTorch first -- only one CPU version!
conda install pytorch torchvision torchaudio -c pytorch

# Install `transformers` as an editable source
pip install -e ".[dev]"

# Install `datasets` as an extra source install
git clone https://github.com/huggingface/datasets
cd datasets
pip install -e .
```