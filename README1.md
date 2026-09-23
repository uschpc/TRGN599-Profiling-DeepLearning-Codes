# Tensorboard

Tensorboard Tutorial Link: https://pytorch.org/tutorials/beginner/introyt/tensorboardyt_tutorial.html



## Run the Jupyter Notebook 
Launch the Jupyter Notebook using OnDemand JupyterLab and run the different code blocks within the jupyter notebook. (You can use the main partition as GPU partition might be busy)


## Tensorboard

TensorBoard is a powerful visualization tool. It provides developers and researchers with insights into their machine learning models by allowing them to visualize metrics, model graphs, and other key aspects of their workflows. Whether you’re debugging a model, tuning hyperparameters, or simply seeking a better understanding of your training process, TensorBoard offers a suite of features to facilitate these tasks.

Some key features of Tensorboard include: 

1 Showing images in TensorBoard

2 Graphing scalers and metrics to visualize training

3 Visualizing your model graphs

## Setup Tensorboard

Launch ‘Terminal’ Apps in OpenOnDemand :

Within the Terminal Apps, change your working direcotry to your scratch directory:
```
cd /scratch2/$(whoami)
```
```
cd CARC/TRGN599-Profiling-DeepLearning-Codes
```


Activate your Conda environment: 
```
conda activate torch-env
```

Launch Tensorboard in your Conda environment: 
```
tensorboard --logdir=runs
```

Right Click on the http://localhost:6006/ link and select ‘Open link’, this will launch a browser and start Tensorboard


Note: if you have issues launching traveler desktop (when you click 'Launch Traveller Desktop', you see a black screen): 
Please go to home directory, go to .config folder and rename xfce4 folder to something like xfce4-old and relaunch another session. 

OR simply remove the folder
```
rm -rf ~/.config/xfce4
```
