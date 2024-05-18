# BenchNIRS

<img title="BenchNIRS" align="right" width="150" height="150" src="https://hanbnrd.gitlab.io/assets/img/logos/benchnirs.png" alt="BenchNIRS">

*Benchmarking framework for machine learning with fNIRS*

> ⚠️ This is only a placeholder, the official *BenchNIRS* repository is hosted [**here**](https://gitlab.com/HanBnrd/benchnirs) ⚠️

**Quick links**  
&rarr; [*Journal article*](https://www.frontiersin.org/articles/10.3389/fnrgo.2023.994969)  
&rarr; [*BenchNIRS repository*](https://gitlab.com/HanBnrd/benchnirs)  
&rarr; [*Install BenchNIRS*](https://hanbnrd.gitlab.io/benchnirs/install.html)  
&rarr; [*Documentation*](https://hanbnrd.gitlab.io/benchnirs)  
&rarr; [*Issue tracker*](https://gitlab.com/HanBnrd/benchnirs/-/issues)  


[![DOI](https://img.shields.io/badge/doi-10.3389%2Ffnrgo.2023.994969-blue)](https://doi.org/10.3389/fnrgo.2023.994969)
[![License](https://img.shields.io/badge/license-GNU%20GPLv3%2b-lightgrey)](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/LICENSE)
[![Pipeline](https://gitlab.com/HanBnrd/benchnirs/badges/main/pipeline.svg)](https://gitlab.com/HanBnrd/benchnirs)
[![PyPI version](https://img.shields.io/pypi/v/benchnirs)](https://pypi.org/project/benchnirs/)
[![Downloads](https://static.pepy.tech/badge/benchnirs)](https://pepy.tech/project/benchnirs)


![Example of figure](https://gitlab.com/HanBnrd/benchnirs/-/raw/v1.0/example.png)


**Features**
- loading of open access datasets
- signal processing and feature extraction on fNIRS data
- training, optimisation and evaluation of machine learning models (including deep learning)
- production of training graphs, metrics and other useful figures for evaluation
- benchmarking and comparison of machine learning models
- supervised, self-supervised and transfer learning
- much more!


## Documentation
The documentation of the framework with examples can be found [here](https://hanbnrd.gitlab.io/benchnirs).


## Recommendation checklist
A checklist of recommendations towards good practice for machine learning with fNIRS (for brain-computer interface applications) can be found [here](./CHECKLIST.md). We welcome contributions from the community in order to improve it, please see below for more information on how to contribute.


## Minimum tested requirements
[**Python 3.8**](https://www.python.org/downloads/) with the following libraries:
- [matplotlib 3.3](https://matplotlib.org/stable/)
- [mne 0.23](https://mne.tools/stable/install/index.html)
- [nirsimple 0.1](https://github.com/HanBnrd/NIRSimple#installation)
- [numpy 1.19](https://numpy.org/install/)
- [pandas 1.0](https://pandas.pydata.org/docs/getting_started/index.html#installation)
- [scikit-learn 0.24](https://scikit-learn.org/stable/install.html)
- [scipy 1.8](https://scipy.org/install/)
- [seaborn 0.11](https://seaborn.pydata.org/installing.html)
- [statsmodels 0.12.2](https://www.statsmodels.org/dev/install.html)
- [torch 1.5](https://pytorch.org/get-started/locally/)


## Setting up *BenchNIRS*
1. Download and install Python 3.8 or greater, for example with [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/index.html).

2. To install the package with *pip* (cf. [PyPI](https://pypi.org/project/benchnirs/)), open a terminal (eg. Anaconda Prompt) and type:
```bash
pip install benchnirs
```
> Alternatively to install from source, download and unzip the [repository](https://gitlab.com/HanBnrd/benchnirs/-/archive/main/benchnirs-main.zip).
> Then, in a terminal or command prompt (eg. Anaconda Prompt), navigate to the directory containing the `requirements.txt` file and run:
> ```bash
> python -m pip install -r requirements.txt -f https://download.pytorch.org/whl/torch_stable.html
> ```

3. Download the datasets (see below).


## Downloading the datasets
- *Herff et al. 2014* (n-back task): you can download the dataset by making a request [here](http://www.csl.uni-bremen.de/CorpusData/download.php?crps=fNIRS). In the examples, the unzipped folder has been renamed to *dataset_herff_2014* for convenience.
- *Shin et al. 2018* (n-back and word generation tasks): you can download the dataset [here](http://doc.ml.tu-berlin.de/simultaneous_EEG_NIRS/NIRS/NIRS_01-26_MATLAB.zip). In the examples, the unzipped folder has been renamed to *dataset_shin_2018* for convenience.
- *Shin et al. 2016* (mental arithmetic task): you can download the dataset by filling the form [here](http://doc.ml.tu-berlin.de/hBCI). Then click on *NIRS_01-29* to download the fNIRS data. In the examples, the unzipped folder has been renamed to *dataset_shin_2016* for convenience.
- *Bak et al. 2019* (motor execution task): you can download the dataset [here](https://figshare.com/ndownloader/files/18069143). In the examples, the unzipped folder has been renamed to *dataset_bak_2019* for convenience.


## Keeping *BenchNIRS* up to date
To update *BenchNIRS* to the latest version with *pip*, open a terminal (eg. Anaconda Prompt) and type:
```bash
pip install --upgrade benchnirs
```


## Example
A full example script showing how to use the framework with a custom deep learning model can be found [here](https://hanbnrd.gitlab.io/benchnirs/example.html).


## Simple use case
*BenchNIRS* enables to evaluate your model in Python with simplicity on an open access dataset supported:
```python
import benchnirs as bn

epochs = bn.load_dataset('shin_2018_nb')
data = bn.process_epochs(epochs['0-back', '2-back', '3-back'])
results = bn.deep_learn(*data, my_model)

print(results)
```


## Running main scripts
- [`generalised.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/generalised.py) compares the 6 models (LDA, SVC, kNN, ANN, CNN and LSTM) on the 5 datasets with a generalised approach (testing with unseen subjects)
- [`dataset_size.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/dataset_size.py) reproduces `generalised.py` but with a range of different dataset sizes (50% to 100% of dataset) to study the influence of this parameter on the classification accuracy
- [`window_size.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/window_size.py) reproduces `generalised.py` but with only the 4 models using feature extraction (LDA, SVC, kNN and ANN) and with a range of different window sizes (2 to 10 seconds) to study the influence of this parameter on the classification accuracy
- [`sliding_window.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/sliding_window.py) reproduces `generalised.py` but with only the 4 models using feature extraction (LDA, SVC, kNN and ANN) and with a 2-second sliding window on the 10-second epochs
- [`personalised.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/personalised.py) compares the 6 models (LDA, SVC, kNN, ANN, CNN and LSTM) on the 5 datasets with a personalised approach (training and testing with each subject individually)
- [`visualisation.py`](https://gitlab.com/HanBnrd/benchnirs/-/blob/main/src/visualisation.py) enables to visualise the data from the datasets with various signal processing


## Extra scripts: n-back tailored
- `tailored_generalised.py` compares the 6 models (LDA, SVC, kNN, ANN, CNN and LSTM) on the 2 n-back datasets with a generalised approach (testing with unseen subjects)
- `tailored_window_size.py` reproduces `tailored_generalised.py` but with only 5 models (LDA, SVC, kNN, ANN and LSTM) and with a range of different window sizes (5 to 40 seconds) to study the influence of this parameter on the classification accuracy
- `tailored_shin_nb.py` optimises and evaluates a tailored CNN on the *Shin et al. 2018* n-back dataset with a generalised approach (testing with unseen subjects)


## Extra scripts: transfer learning
- `transfer.py` optimises and evaluates a transfer learning model (pretext self-supervised representation learning task with unlabelled and labelled data using a CED, downstream supervised n-back classification task with labelled data) on the *Shin et al. 2018* n-back dataset with a generalised approach (testing with unseen subjects)
- `transfer_no_unlab.py` reproduces `transfer.py` but with only labelled data for the pretext task.


## Contributing to the repository
Contributions from the community to this repository are highly appreciated. We are mainly interested in contributions to:
- improving the recommendation checklist
- adding support for new open access datasets
- adding support for new machine learning models
- adding more fNIRS signal processing techniques
- improving the documentation
- tracking bugs

Contributions are encouraged under the form of [issues](https://gitlab.com/HanBnrd/benchnirs/-/issues) (for reporting bugs or requesting new features) and [merge requests](https://gitlab.com/HanBnrd/benchnirs/-/merge_requests) (for fixing bugs and implementing new features).
Please refer to [this tutorial](https://docs.gitlab.com/ee/user/project/repository/forking_workflow.html) for creating merge requests from a fork of the repository.


## Acknowledgements
If you are using *BenchNIRS*, please cite [this article](https://doi.org/10.3389/fnrgo.2023.994969>):
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
> 
> [*Herff et al. 2014*](https://doi.org/10.3389/fnhum.2013.00935)
> ```
> @article{herff2014mental,
> 	title={Mental workload during n-back task—quantified in the prefrontal cortex using fNIRS},
> 	author={Herff, Christian and Heger, Dominic and Fortmann, Ole and Hennrich, Johannes and Putze, Felix and Schultz, Tanja},
> 	journal={Frontiers in human neuroscience},
> 	volume={7},
> 	pages={935},
> 	year={2014},
> 	publisher={Frontiers}
> }
> ```
> 
> [*Shin et al. 2018*](https://doi.org/10.1038/sdata.2018.3)
> ```
> @article{shin2018simultaneous,
> 	title={Simultaneous acquisition of EEG and NIRS during cognitive tasks for an open access dataset},
> 	author={Shin, Jaeyoung and Von L{\"u}hmann, Alexander and Kim, Do-Won and Mehnert, Jan and Hwang, Han-Jeong and M{\"u}ller, Klaus-Robert},
> 	journal={Scientific data},
> 	volume={5},
> 	pages={180003},
> 	year={2018},
> 	publisher={Nature Publishing Group}
> }
> ```
> 
> [*Shin et al. 2016*](https://doi.org/10.1109/TNSRE.2016.2628057)
> ```
> @article{shin2016open,
> 	title={Open access dataset for EEG+NIRS single-trial classification},
> 	author={Shin, Jaeyoung and von L{\"u}hmann, Alexander and Blankertz, Benjamin and Kim, Do-Won and Jeong, Jichai and Hwang, Han-Jeong and M{\"u}ller, Klaus-Robert},
> 	journal={IEEE Transactions on Neural Systems and Rehabilitation Engineering},
> 	volume={25},
> 	number={10},
> 	pages={1735--1745},
> 	year={2016},
> 	publisher={IEEE}
> }
> ```
> 
> [*Bak et al. 2019*](https://doi.org/10.3390/electronics8121486)
> ```
> @article{bak2019open,
> 	title={Open-Access fNIRS Dataset for Classification of Unilateral Finger-and Foot-Tapping},
> 	author={Bak, SuJin and Park, Jinwoo and Shin, Jaeyoung and Jeong, Jichai},
> 	journal={Electronics},
> 	volume={8},
> 	number={12},
> 	pages={1486},
> 	year={2019},
> 	publisher={Multidisciplinary Digital Publishing Institute}
> }
> ```
