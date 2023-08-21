Installing Tensorflow compatible with NVIDIA GPUs on Alpine:
============================================================

This short tutorial will guide you through installing Tensorflow on Alpine compatible with NVIDIA A100 acceleration.

## Tensorflow installation steps.

1) After you log into the Alpine cluster, please load the Slurm modules and request allocation so that you can install the packages:

```bash
module load slurm/alpine 
acompile --ntasks=4 --time=01:30:00
```

2) Load anaconda, create your environment with python 3.9 and activate it.

```bash
module load anaconda
conda create -n tf_env python=3.9 
conda activate tf_env
```

3) Install cudnn 8.6.0

```bash
pip install nvidia-cudnn-cu11==8.6.0.163 
```

4) Install cuda-toolkit 11.8.0

```bash
conda install -c "nvidia/label/cuda-11.8.0" cuda-toolkit 
```

5) Install Tensorflow 2.12.0. Also note that tensorflow, cuda and cudnn have to follow a strict versioning:
   https://www.tensorflow.org/install/source#gpu

```bash
python3 -m pip install tensorflow==2.12.0
```

6) Export the correct paths by following this guide here: https://www.tensorflow.org/install/pip

```bash
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
echo 'CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
echo 'export LD_LIBRARY_PATH=$CONDA_PREFIX/lib/:$CUDNN_PATH/lib:$LD_LIBRARY_PATH' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
source $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
export LD_LIBRARY_PATH=$CONDA_PREFIX/lib/python3.9/site-packages/nvidia/cudnn/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$CONDA_PREFIX/lib:$LD_LIBRARY_PATH
export PATH=$CONDA_PREFIX/bin:$PATH
export XLA_FLAGS=--xla_gpu_cuda_data_dir=$CONDA_PREFIX
```

7) Install Tensorrt and export PATH:

```bash
pip install nvidia-tensorrt==8.4.1.5
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/python3.9/site-packages/tensorrt
```

8) We link libnvinfer.so.8  to libnvinfer.so.7 :

```bash
ln -s $CONDA_PREFIX/lib/python3.9/site-packages/tensorrt/libnvinfer.so.8 $CONDA_PREFIX/lib/python3.9/site-packages/tensorrt/libnvinfer.so.7
ln -s $CONDA_PREFIX/lib/python3.9/site-packages/tensorrt/libnvinfer_plugin.so.8  $CONDA_PREFIX/lib/python3.9/site-packages/tensorrt/libnvinfer_plugin.so.7 
```

9) To test that your installation is working you will need to exit "acompile"  first and load on the NVIDIA GPU debug partition on Alpine"

```bash
conda deactivate
exit
sinteractive --partition=atesting_a100 --qos=testing --time=00:05:00 --gres=gpu:1 --ntasks=2
module load anaconda
conda activate tf_env
python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

10) Make sure to exit the GPU debug node partition after testing the installation.
   
```bash
$ exit
exit
```
