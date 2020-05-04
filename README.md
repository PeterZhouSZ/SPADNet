## SPADNet
[SPADnet: Deep RGB-SPAD Sensor Fusion Assisted by Monocular Depth Estimation]. 

[SPADnet: Deep RGB-SPAD Sensor Fusion Assisted by Monocular Depth Estimation]: https://www.osapublishing.org/oe/abstract.cfm?uri=oe-28-10-14948


Created by Zhanghao Sun, David Brian Lindell, [Olav Solgaard] and [Gordon Wetzstein] from Stanford University.

**We will make code and pre-trained model public soon.**

[Olav Solgaard]: https://solgaardlab.stanford.edu/#research
[Gordon Wetzstein]: http://www.computationalimaging.org

## Introduction
This repository is code release for our Optics Express paper "SPADnet: Deep RGB-SPAD Sensor Fusion Assisted by Monocular Depth Estimation". 

Construction of 3D scenes is essential for many applications. An emerging technique, single-photon-avalanche-diode (SPAD)-based 3D imaging, is attracting increasing attention. In this work, we aim at depth reconstruction from noisy SPAD measurements. Previous algorithms generally suffer from insufficient accuracy under low photon-flux conditions. 

In this paper, we introduce SPADnet—a neural network architecture for robust RGB-SPAD sensor fusion. We introduce monocular depth estimation into the network to assist the fusion process and also optimize the training procedure with a better objective function and log-scale rebinning. The proposed model achieves state-of-the-art performance in SPAD denoising. It is also more memory efficient and significantly faster than previous RGB-SPAD fusion approaches. This work can lead to the application of SPAD-based 3D reconstruction in broader contexts, such as 3D imaging with longer range and strong ambient light or 3D imaging on mobile devices. Also, the general insight that monocular depth estimator can facilitate fusion between 3D and 2D data modality may be helpful in other 3D sensing related scenarios.

For more details of our work, please refer to our technical paper.

## Citation
If you find our work useful in your research, please consider citing:


## Installation
We use Python 3.6 , Pytorch 1.0 and CUDA 9.0 for our experiments. One can install our conda environment from "environment.yml".

## Training
### Preparing data
We use [NYUV2] dataset for SPAD measurement simulation. We select out data with high quality (without large holes in ground truth depth map, with reasonable reflectivity value and so on), which are separated into training set, validation set and test set (10:1:1). Corresponding scene index are listed in "util/train_clean.txt", "util/val_clean.txt" and "util/test_clean.txt".

To simulate SPAD measurements, we use NYUV2 toolkit and code from [Lindell et al., 2018]. A signal-background ratio (SBR) needs to be specified for simulation. We always use the lowest SBR (2 signal photons and 50 background photons) during experiments and observed good generalization capability to complicated real-world scenes.

Our scripts directly load monocular estimation results. We use [DORN] model as monocular estimation network for most part of the work and [here] we provide corresponding estimation results. Users can replace them with any other preliminary depth estimations.
[Lindell et al., 2018]: http://www.computationalimaging.org/publications/single-photon-3d-imaging-with-deep-sensor-fusion/
[here]: 

### Model training
One can train SPADnet model from scratch by running:
sh scripts/command_train.sh
after both SPAD simulation and corresponding monocular depth estimations are completed. We use Adam Optimizer, with a learning rate of 1e-4 and learning rate decay of 0.5 after each epoch. The whole training process has 5 epochs and would take around 24hrs on Nvidia Titan V GPU (12GB).

We also provide a pre-trained snapshot of SPADnet model [Here] (12.5MB).

[NYUV2]: https://cs.nyu.edu/~silberman/datasets/nyu_depth_v2.html
[Here]: https://drive.google.com/file/d/1KDzbRpT_HA0Y0lEtPabKKlUhgcQ40FWr/view?usp=sharing

## Evaluation
### Simulated Dataset
One can evaluate SPADnet model on simulated NYUV2 dataset by running:
sh scripts/command_eval.sh

### Real-world Captured Dataset
We also evaluate our model on real-world captured SPAD data. We provide SPAD measurements as well as scaled monocular depth estimations for three different scenes [Here]. For monocular estimations, we provide the results from two SOTA networks: [DenseDepth] and [DORN].
[Here]: 
[DenseDepth]: https://arxiv.org/abs/1812.11941
[DORN]: http://openaccess.thecvf.com/content_cvpr_2018/html/Fu_Deep_Ordinal_Regression_CVPR_2018_paper.html

