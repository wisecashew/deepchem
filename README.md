﻿# DeepChem

[![Build Status](https://travis-ci.org/deepchem/deepchem.svg?branch=master)](https://travis-ci.org/deepchem/deepchem)
[![Coverage Status](https://coveralls.io/repos/github/deepchem/deepchem/badge.svg?branch=master)](https://coveralls.io/github/deepchem/deepchem?branch=master)
[![Anaconda-Server Badge](https://anaconda.org/deepchem/deepchem/badges/version.svg)](https://anaconda.org/deepchem/deepchem)
[![PyPI version](https://badge.fury.io/py/deepchem.svg)](https://badge.fury.io/py/deepchem)

Documentation ([Latest](https://deepchem.readthedocs.io/en/latest/))

DeepChem aims to provide a high quality open-source toolchain
that democratizes the use of deep-learning in drug discovery,
materials science, quantum chemistry, and biology.

### Table of contents:

- [Requirements](#requirements)
- [Installation](#installation)
  - [Install latest package with conda](#install-via-conda-recommendation)
  - [Install latest package with pip (WIP)](#install-via-pip-wip)
  - [Install from source](#install-from-source)
    - [General installation](#general-installation)
    - [Use powershell (Windows)](#use-powershell-windows)
  - [Install using a Docker (WIP)](#install-using-a-docker-wip)
- [FAQ and Troubleshooting](#faq-and-troubleshooting)
- [Getting Started](#getting-started)
- [Contributing to DeepChem](/CONTRIBUTING.md)
  - [Code Style Guidelines](/CONTRIBUTING.md#code-style-guidelines)
  - [Documentation Style Guidelines](/CONTRIBUTING.md#documentation-style-guidelines)
  - [Gitter](#gitter)
- [DeepChem Publications](#deepchem-publications)
- [Examples](/examples)
- [About Us](#about-us)
- [Citing DeepChem](#citing-deepchem)

## Requirements

DeepChem requires these packages on any condition.

- [joblib](https://pypi.python.org/pypi/joblib)
- [NumPy](https://numpy.org/)
- [pandas](http://pandas.pydata.org/)
- [scikit-learn](https://scikit-learn.org/stable/)
- [SciPy](https://www.scipy.org/)
- [TensorFlow](https://www.tensorflow.org/)
  - `deepchem>=2.4.0` requires tensorflow v2
  - `deepchem<2.4.0` requires tensorflow v1

### Soft Requirements

DeepChem has a number of "soft" requirements. These are packages which are needed for various submodules of DeepChem but not for the package as a whole.

- [BioPython](https://biopython.org/wiki/Documentation)
- [OpenAI Gym](https://gym.openai.com/)
- [MDTraj](http://mdtraj.org/)
- [NetworkX](https://networkx.github.io/documentation/stable/index.html)
- [OpenMM](http://openmm.org/)
- [PDBFixer](https://github.com/pandegroup/pdbfixer)
- [Pillow](https://pypi.org/project/Pillow/)
- [pyGPGO](https://pygpgo.readthedocs.io/en/latest/)
- [PyTorch](https://pytorch.org/)
- [RDKit](http://www.rdkit.org/docs/Install.html)
- [simdna](https://github.com/kundajelab/simdna)
- [XGBoost](https://xgboost.readthedocs.io/en/latest/)

## Installation

### Install via conda (Recommendation)

RDKit is a soft requirement package, but many useful methods like molnet are dependent on it.
If you use conda, we recommend installing RDKit with deepchem.

`deepchem>=2.4.0`

Coming soon...

`deepchem<2.4.0`

```bash
pip install tensorflow==1.14
conda install -c rdkit -c conda-forge rdkit deepchem==2.3.0
```

If you want GPU support:

```bash
pip install tensorflow-gpu==1.14
conda install -c rdkit -c conda-forge rdkit deepchem==2.3.0
```

### Install via pip (WIP)

You are able to try to install deepchem via pip using the following command.  
However, pip installation is under development, so this command may not work well.

`deepchem>=2.4.0`

Coming soon...

`deepchem<2.4.0`

```bash
pip install pandas pillow scikit-learn==0.22 tensorflow==1.14 deepchem==2.2.1.dev54
```

If you want GPU support:

```bash
pip install pandas pillow scikit-learn==0.22 tensorflow-gpu==1.14 deepchem==2.2.1.dev54
```

### Install from source

You can install deepchem in a new conda environment using the conda commands in `scripts/install_deepchem_conda.sh.` Installing via this script will ensure that you are **installing from the source**.  
The following script requires `conda>=4.4` because it uses the `conda activate` command. (Please see the detail from [here](https://github.com/conda/conda/blob/a4c4feae404b2b378e106bd25f62cc8be15c768f/CHANGELOG.md#440-2017-12-20))

First, please clone the deepchem repository from GitHub.

```bash
git clone https://github.com/deepchem/deepchem.git
cd deepchem
```

Then, follow each instruction on your OS.

### General installation

```bash
bash scripts/install_deepchem_conda.sh deepchem
```

Before activating deepchem environment, make sure conda has been initialized.  
Check if there is a `(base)` in your command line. If not, use `conda init bash` to activate it, then:

```
conda activate deepchem
python setup.py install
pytest -m "not slow"
```

Check [this link](https://conda.io/projects/conda/en/latest/user-guide/install/index.html) for more information about the installation of conda environments.

### Use powershell (Windows)

Currently you have to install from source in windows.

```ps1
.\scripts\install_deepchem_conda.ps1 deepchem
```

Before activating deepchem environment, make sure conda-powershell has been initialized.  
Check if there is a `(base)` before `PS` in powershell. If not, use `conda init powershell` to activate it, then:

```bash
conda activate deepchem
python setup.py install
pytest -m "not slow"
```

### Install using a Docker (WIP)

### Build the image from Dockerfile

We created [sample Dockerfiles](https://github.com/deepchem/deepchem/tree/master/docker) based on the `nvidia/cuda:10.1-cudnn7-devel` image.  
If you want to build your own deepchem environment, these files may be helpful.  
- `docker/x.x.x` : build an image by using conda package manager (x.x.x is a version of deepchem)  
- `docker/master` : build an image from master branch of deepchem source codes

### Use the official deepchem image (WIP)

We couldn't check if this introduction works well or not.

First, you pull the latest stable deepchem docker image.

```bash
docker pull deepchemio/deepchem
```

Then, you create a container based on our latest image.

```bash
docker run -it deepchemio/deepchem
```

If you want GPU support:

```bash
# If nvidia-docker is installed
nvidia-docker run -it deepchemio/deepchem
docker run --runtime nvidia -it deepchemio/deepchem

# If nvidia-container-toolkit is installed
docker run --gpus all -it deepchemio/deepchem
```

You are now in a docker container whose python has deepchem installed.

```bash
# you can start playing with it in the command line
pip install jupyter
ipython
import deepchem as dc

# you can run our tox21 benchmark
cd /deepchem/examples
python benchmark.py -d tox21
```

## FAQ and Troubleshooting

1. DeepChem currently supports Python 3.5 through 3.7, and is supported on 64 bit Linux and Mac OSX. Note that DeepChem is not currently maintained for older versions of Python or with other operating systems.
2. Question: I'm seeing some failures in my test suite having to do with MKL
   `Intel MKL FATAL ERROR: Cannot load libmkl_avx.so or libmkl_def.so.`

   Answer: This is a general issue with the newest version of `scikit-learn` enabling MKL by default. This doesn't play well with many linux systems. See [BVLC/caffe#3884](https://github.com/BVLC/caffe/issues/3884) for discussions. The following seems to fix the issue

   ```bash
   conda install nomkl numpy scipy scikit-learn numexpr
   conda remove mkl mkl-service
   ```

3. Note that when using Ubuntu 16.04 server or similar environments, you may need to ensure libxrender is provided via e.g.:

```bash
sudo apt-get install -y libxrender-dev
```

## Getting Started

The DeepChem project maintains an extensive colelction of [tutorials](https://github.com/deepchem/deepchem/tree/master/examples/tutorials). All tutorials are designed to be run on Google colab (or locally if you prefer). Tutorials are arranged in a suggested learning sequence which will take you from beginner to proficient at molecular machine learning and computational biology more broadly.

After working through the tutorials, you can also go through other [examples](https://github.com/deepchem/deepchem/tree/master/examples). To apply `deepchem` to a new problem, try starting from one of the existing examples or tutorials and modifying it step by step to work with your new use-case. If you have questions or comments you can raise them on our [gitter](https://gitter.im/deepchem/Lobby).

### Gitter

Join us on gitter at [https://gitter.im/deepchem/Lobby](https://gitter.im/deepchem/Lobby). Probably the easiest place to ask simple questions or float requests for new features.

## About Us

DeepChem is managed by a team of open source contributors. Anyone is free to join and contribute!

## Citing DeepChem

If you have used DeepChem in the course of your research, we ask that you cite the "Deep Learning for the Life Sciences" book by the DeepChem core team.

To cite this book, please use this bibtex entry:

```
@book{Ramsundar-et-al-2019,
    title={Deep Learning for the Life Sciences},
    author={Bharath Ramsundar and Peter Eastman and Patrick Walters and Vijay Pande and Karl Leswing and Zhenqin Wu},
    publisher={O'Reilly Media},
    note={\url{https://www.amazon.com/Deep-Learning-Life-Sciences-Microscopy/dp/1492039837}},
    year={2019}
}
```

## Version

2.1.0
