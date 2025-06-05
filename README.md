# BenchNIRS

<img title="BenchNIRS" align="right" width="150" height="150" src="https://hanbnrd.gitlab.io/assets/img/logos/benchnirs.png" alt="BenchNIRS">

*Benchmarking framework for machine learning with fNIRS*

> ⚠️ This is only a placeholder, the official *BenchNIRS* repository is hosted [**here**](https://gitlab.com/HanBnrd/benchnirs) ⚠️

**Quick links**  
&rarr; [*Journal article*](https://www.frontiersin.org/articles/10.3389/fnrgo.2023.994969)  
&rarr; [*BenchNIRS source code*](https://gitlab.com/HanBnrd/benchnirs)  
&rarr; [*Install BenchNIRS*](https://hanbnrd.gitlab.io/benchnirs/install.html)  
&rarr; [*Documentation*](https://hanbnrd.gitlab.io/benchnirs)  
&rarr; [*Examples*](https://hanbnrd.gitlab.io/benchnirs/examples.html)  
&rarr; [*Issue tracker*](https://gitlab.com/HanBnrd/benchnirs/-/issues)  


[![PyPI version](https://img.shields.io/pypi/v/benchnirs)](https://pypi.org/project/benchnirs/)
[![License](https://img.shields.io/badge/license-MIT-blue)](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/LICENSE)
[![DOI](https://img.shields.io/badge/doi-10.3389%2Ffnrgo.2023.994969-blue)](https://doi.org/10.3389/fnrgo.2023.994969)


![Example of figure](https://gitlab.com/HanBnrd/benchnirs/-/raw/v1.0/example.png)


**Features**
- loading of open access datasets
- signal processing and feature extraction on fNIRS data
- training, hyperparameter tuning and evaluation of machine learning models (including deep learning)
- production of training graphs, metrics and other useful figures for evaluation
- benchmarking and comparison of machine learning models
- much more!


## Documentation
The documentation of the framework with examples can be found [here](https://hanbnrd.gitlab.io/benchnirs).


## Recommendation checklist
A checklist of recommendations towards best practices for machine learning with fNIRS can be found [here](./CHECKLIST.md). We welcome contributions from the community in order to improve it, please see below for more information on how to contribute.


## Setting up *BenchNIRS*
1. Download and install Python 3.9 or greater, for example with [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/index.html).

2. To install the package with *pip* (cf. [PyPI](https://pypi.org/project/benchnirs/)), open a terminal (eg. Anaconda Prompt) and type:
```bash
pip install benchnirs
```

3. Download the datasets (see below).

> Alternatively to install from source in development mode, download and unzip the [repository](https://gitlab.com/HanBnrd/benchnirs/-/archive/main/benchnirs-main.zip) (or clone it with Git), and run `devinstall.py`.


## Downloading datasets
- *Herff et al. 2014* (n-back task): you can download the dataset by making a request [here](http://www.csl.uni-bremen.de/CorpusData/download.php?crps=fNIRS).
- *Shin et al. 2018* (n-back and word generation tasks): you can download the dataset [here](http://doc.ml.tu-berlin.de/simultaneous_EEG_NIRS/NIRS/NIRS_01-26_MATLAB.zip).
- *Shin et al. 2016* (mental arithmetic task): you can download the dataset by filling out the form [here](http://doc.ml.tu-berlin.de/hBCI). Then click on *NIRS_01-29* to download the fNIRS data.
- *Bak et al. 2019* (motor execution task): you can download the dataset [here](https://figshare.com/ndownloader/files/18069143).


## Keeping *BenchNIRS* up to date
To update *BenchNIRS* to the latest version with *pip*, open a terminal (eg. Anaconda Prompt) and type:
```bash
pip install --upgrade benchnirs
```


## Examples
A set of example scripts showing how to use the framework can be found [here](https://hanbnrd.gitlab.io/benchnirs/examples.html).


## Simple use case
Define a model with PyTorch:
```python
import torch.nn as nn
import torch.nn.functional as F


class MyModel(nn.Module):

    def __init__(self, n_classes):
        super().__init__()
        self.fc1 = nn.Linear(400, 250)
        self.fc2 = nn.Linear(250, 150)
        self.fc3 = nn.Linear(150, 60)
        self.fc4 = nn.Linear(60, n_classes)

    def forward(self, x):
        batch_size = x.size(0)
        x = x.view(batch_size, -1)  # flatten
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = F.relu(self.fc3(x))
        x = self.fc4(x)
        return x
```
Evaluate the model on one of the datasets:
```python
import benchnirs as bn

# Download dataset: https://figshare.com/ndownloader/files/18069143

# Load and process data:
epochs = bn.load_dataset('bak_2019_me', roi_sides=True, path='./bak_2019')
data = bn.process_epochs(epochs['right', 'left', 'foot'])

# Benchmark model:
results = bn.deep_learn(MyModel, *data)
print(results)
```


## Contributing
Contributions to this repository are very welcome under the form of [issues](https://gitlab.com/HanBnrd/benchnirs/-/issues) (for reporting bugs or requesting new features) and [merge requests](https://gitlab.com/HanBnrd/benchnirs/-/merge_requests) (for fixing bugs and implementing new features).
Please refer to [this tutorial](https://docs.gitlab.com/ee/user/project/repository/forking_workflow.html) for creating merge requests from a fork of the repository.


## Contributors
Johann Benerradi &bull; Jeremie Clos &bull; Aleksandra Landowska &bull; Michel F. Valstar &bull; Max L. Wilson &bull; Yujie Yao


## Acknowledgements
If you are using *BenchNIRS*, please cite [this article](https://doi.org/10.3389/fnrgo.2023.994969):
```
@article{benerradi2023benchmarking,
  title={Benchmarking framework for machine learning classification from fNIRS data},
  author={Benerradi, Johann and Clos, Jeremie and Landowska, Aleksandra and Valstar, Michel F and Wilson, Max L},
  journal={Frontiers in Neuroergonomics},
  volume={4},
  year={2023},
  publisher={Frontiers Media},
  url={https://www.frontiersin.org/articles/10.3389/fnrgo.2023.994969},
  doi={10.3389/fnrgo.2023.994969},
  issn={2673-6195}
}
```

> If you are using the datasets of the framework, please also cite those related works:
> - [*Herff et al. 2014*](https://doi.org/10.3389/fnhum.2013.00935)
> - [*Shin et al. 2018*](https://doi.org/10.1038/sdata.2018.3)
> - [*Shin et al. 2016*](https://doi.org/10.1109/TNSRE.2016.2628057)
> - [*Bak et al. 2019*](https://doi.org/10.3390/electronics8121486)
