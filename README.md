# V1TA: Adapting the Allen Brain Observatory Dataset to V1T Model

## Introduction

**V1TA** is a project that adapts the **Allen Brain Observatory Dataset** to work with **V1T**.

V1T is a neural network model based on the Vision Transformer architecture. It was developed by **Bryan M. Li et al.** and trained to model how neurons in mouse respond to visual input. It was originally tested on datasets like **Sensorium** and **Franke et al. 2022**, which include both visual stimuli and neural recordings.

The Allen Brain Observatory, from the **Allen Institute for Brain Science**, is a public dataset that contains large-scale recordings of mouse visual cortex activity using **two-photon calcium imaging**. Mice are shown a variety of visual stimuli (e.g., natural scenes, gratings, movies), and their brain activity is recorded.

## Process

An in-detail showcase of our process is available in the `Presentazione V1TA.pdf` file. We highly recommend checking it out. The following is a brief summary of the project.


### Allen Dataset Adaptation

The original V1T pipeline and the Allen dataset have very different formats, so we made several modifications:

- 📐 **Image resizing**:  
  - Original stimuli were **918×1174 pixels**.  
  - We resized them to **144×256**.

- 🧠 **Neural activity processing**:  
  - Calcium signals (ΔF/F) were averaged over **500 ms windows**.  
  - The data was saved in `.npy` format.

- ⚙️ **Metadata adjustments**:  
  - Created metadata files for `unit_ids.npy` and `cell_motor_coordinates.npy`.  
  - Manually computed statistics (mean, standard deviation, max) for normalization.

To integrate the Allen dataset into the V1T model, we made key updates:

- 📁 **Data loader updates (`data.py` file)**:  
  - Added support for `"allen"` as a valid dataset option.

### Training

After multiple training sessions, the best performance (measured by correlation between predicted and actual neural responses) was:

- 📊 **Correlation**: `0.16`
- ⚙️ **Hyperparameters**:
  - Learning rate (core): `0.004`
  - Learning rate (readout): `0.007`
  - Batch size: `16`
  - Loss function: **Poisson Loss**

## Conclusions


- Showed that the **V1T model can be adapted** to work with new, non-native datasets like Allen.
- Our preprocessing and code changes allow future expansion (e.g., including pupil data if it becomes available).

- Model performance is lower than with the original datasets. This is likely due to **missing behavioral features**, such as **pupil dilation**, which influence brain activation of the V1 area.

## Sources
- 📄 **Original V1T Paper**  
  [*Li, Bryan M., et al. “V1T: A Vision Transformer for Neural System Identification.” NeurIPS 2023.* ](https://openreview.net/forum?id=pvqQZGtdltd)
- 🧠 **Allen Brain Observatory Dataset**  
  [*Allen Brain Observatory: Visual Coding - 2P Dataset*](https://portal.brain-map.org/explore/circuits/visual-coding-2p)
- 🤖 **Original V1T Repository**    
 [*Code for "V1T: Large-scale mouse V1 response prediction using a Vision Transformer"*](https://github.com/bryanlimy/V1T)

 ## Authors

- **Fernando Riccioli**
- **Nunzio Fornitto**
- **Angelo Frasca**

And special thanks to:
- **Salvatore Calcagno** for supervising and contributing to the project.
- **Bryan M. Li** for directions, support and contribution.