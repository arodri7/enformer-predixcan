# Enformer - Predixcan on Summit OLCF

Goal is to install and have running [Enformer](https://github.com/deepmind/deepmind-research/tree/master/enformer) and Predixcan version on the Summit machines.


Since installing things like PyTorch, tensorflow, etc. on Summit is extremely complicated to install, OLCF provides common ML/DL libraries in an OpenCE Anaconda environment. 
See this links that is an overview of our [OpenCE environment](https://docs.olcf.ornl.gov/software/analytics/ibm-wml-ce.html)

That takes care of the tensorflow requirement, but that environment does not include "Enformer", so you'll still have to try and install that in a custom conda environment. 
Since you can't install additional packages into the default OpenCE environment, you'll have to make a clone, for example:

```
module load open-ce/1.2.0-py38-0
conda create -n enformer_env --clone open-ce-1.2.0-py38-0
conda activate enformer_env
```

Note, since the open-ce environment is so large, this may take a while to clone. You can then try installing enformer into that environment. 
I wouldn't be surprised if there are issues, with how complex Summit is, but hopefully it will work.

Also, if you ever log out and log back in, you can get back to your new environment without needing to load the open-ce module, and you can just use the regular python module, for example:

```
module load python
source activate enformer_env
```
Summit has a package available
