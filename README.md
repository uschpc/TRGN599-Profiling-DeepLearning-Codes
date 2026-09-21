# TRGN599-Profiling-DeepLearning-Codes

### About
The material in this repo covers how to run deep learning applications in HPC system. You can watch CNN tutorial in this link: https://www.youtube.com/watch?v=bNb2fEVKeEo

# Single-GPU Training

It is important to optimize your script for the single-GPU case before moving to multi-GPU training. This is because as you request more resources, your queue time increases. We also want to avoid wasting resources by running code that is not optimized.

Here we train a CNN on the MNIST dataset using a single GPU as an example. We profile the code and make performance improvements.

## Step 1: Software Environment Setup

Follow the instruction of week3. 

### Clone this repo and start learning how to run deep learning applications in HPC system. 
First login to CARC OnDemand: https://ondemand.carc.usc.edu/ and request a 'Discovery Cluster Shell Access' within OpenOnDemand.

```bash
cd /scratch1/$(whoami)
mkdir CARC
cd CARC
git clone https://github.com/uschpc/TAC450-DataScience-Fall2026
cd TAC450-DataScience-Fall2026/week4
```


## Step 2: Run and Profile the Script

First, inspect the script ([see script](mnist_classify.py)) by running these commands:

```bash
$ cat mnist_classify.py
```

```
Note: nn.Conv2d(1, 32, 3, 1): This is creating a 2D convolutional layer. Here’s a breakdown of the arguments:
(a) 1: The number of input channels. This could be 1 for a grayscale image, 3 for a color image (RGB), etc.
(b) 32: The number of output channels (i.e., the number of filters or kernels). This means that the output of this convolutional layer will have 32 feature maps.
(c) 3: The size of the convolutional kernel (or filter). This means a 3x3 filter is used for the convolution.
(d) 1: The stride of the convolution, which controls how the filter moves across the input. A stride of 1 means the filter moves one pixel at a time.
```

We will profile the `train` function using `line_profiler` by adding the following decorator above the train function:

```python
@profile
def train(args, model, device, train_loader, optimizer, epoch):
```

Below is the Slurm script:

```bash
#!/bin/bash
#SBATCH --job-name=mnist         # create a short name for your job
#SBATCH --partition=gpu          # gpu partition
#SBATCH --nodes=1                # node count
#SBATCH --ntasks=1               # total number of tasks across all nodes
#SBATCH --cpus-per-task=1        # cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --mem=8G                 # total memory per node (4 GB per cpu-core is default)
#SBATCH --gres=gpu:1             # number of gpus per node
#SBATCH --time=00:10:00          # total run time limit (HH:MM:SS)
#SBATCH --account=irahbari_1147  # account name
#SBATCH --reservation=tac-450-th # reservation for ITP class on Thursday
