# Enformer - Predixcan on Summit OLCF

Goal is to install and have running [Enformer](https://github.com/deepmind/deepmind-research/tree/master/enformer) and Predixcan version on the Summit machines.


## Installation
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

To install the remainder packages for Enformer:
```
pip install dm-sonnet==2.0.0
pip install kipoiseq==0.5.2
pip install tensorflow-hub==0.11.0
```

You will need to clone [deepmind's](https://github.com/deepmind/deepmind-research.git) repository:
```
git clone https://github.com/deepmind/deepmind-research.git
cd ~/enformer/deepmind-research/enformer
```

To test the Enformer installation you can run the unit test:

```
(enformer_env) [arodriguez@login1.summit enformer]$ python -m enformer_test
2022-09-28 10:12:05.114257: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-09-28 10:12:11.050434: I tensorflow/compiler/jit/xla_cpu_device.cc:41] Not creating XLA devices, tf_xla_enable_xla_devices not set
2022-09-28 10:12:11.052680: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcuda.so.1
2022-09-28 10:12:11.086303: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1720] Found device 0 with properties:
pciBusID: 0035:04:00.0 name: Tesla V100-SXM2-16GB computeCapability: 7.0
coreClock: 1.53GHz coreCount: 80 deviceMemorySize: 15.75GiB deviceMemoryBandwidth: 836.37GiB/s
2022-09-28 10:12:11.086338: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-09-28 10:12:11.116913: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublas.so.11
2022-09-28 10:12:11.116947: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublasLt.so.11
2022-09-28 10:12:11.130510: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcufft.so.10
2022-09-28 10:12:11.139942: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcurand.so.10
2022-09-28 10:12:11.166478: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcusolver.so.10
2022-09-28 10:12:11.176801: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcusparse.so.11
2022-09-28 10:12:11.180707: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudnn.so.8
2022-09-28 10:12:11.183663: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1862] Adding visible gpu devices: 0
2022-09-28 10:12:11.189146: I tensorflow/compiler/jit/xla_gpu_device.cc:99] Not creating XLA devices, tf_xla_enable_xla_devices not set
2022-09-28 10:12:11.190934: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1720] Found device 0 with properties:
pciBusID: 0035:04:00.0 name: Tesla V100-SXM2-16GB computeCapability: 7.0
coreClock: 1.53GHz coreCount: 80 deviceMemorySize: 15.75GiB deviceMemoryBandwidth: 836.37GiB/s
2022-09-28 10:12:11.190958: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-09-28 10:12:11.190979: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublas.so.11
2022-09-28 10:12:11.190997: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublasLt.so.11
2022-09-28 10:12:11.191012: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcufft.so.10
2022-09-28 10:12:11.191028: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcurand.so.10
2022-09-28 10:12:11.191045: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcusolver.so.10
2022-09-28 10:12:11.191060: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcusparse.so.11
2022-09-28 10:12:11.191077: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudnn.so.8
2022-09-28 10:12:11.194237: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1862] Adding visible gpu devices: 0
2022-09-28 10:12:11.194263: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudart.so.11.0
2022-09-28 10:12:12.318250: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1261] Device interconnect StreamExecutor with strength 1 edge matrix:
2022-09-28 10:12:12.318287: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1267]      0
2022-09-28 10:12:12.318296: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1280] 0:   N
2022-09-28 10:12:12.322617: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1406] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 14787 MB memory) -> physical GPU (device: 0, name: Tesla V100-SXM2-16GB, pci bus id: 0035:04:00.0, compute capability: 7.0)
/ccs/home/arodriguez/.conda/envs/enformer_env/lib/python3.8/site-packages/sonnet/src/utils.py:43: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated since Python 3.3, and in 3.10 it will stop working
  if not isinstance(element, collections.Sequence):
2022-09-28 10:12:12.978134: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcudnn.so.8
2022-09-28 10:12:17.360211: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublas.so.11
2022-09-28 10:12:17.979419: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library libcublasLt.so.11
/ccs/home/arodriguez/.conda/envs/enformer_env/lib/python3.8/site-packages/tree/__init__.py:312: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated since Python 3.3, and in 3.10 it will stop working
  return _tree.flatten(structure)
.
----------------------------------------------------------------------
Ran 1 test in 9.219s

OK
```
