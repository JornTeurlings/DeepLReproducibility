# Reproducting "Data-driven Feature Tracking for Event Cameras"
Authors:

- Jorn Teurlings 4956818
- Xiaotong Li
- Ziang Liu
- Siqi Pei
 


## Introduction
In the realm of computer vision and augmented/virtual reality (AR/VR), the challenge of effectively tracking features in high-speed motion scenes is a pivotal concern, especially as AR/VR devices become increasingly common. Standard cameras, the typical choice for these applications, face significant limitations due to the bandwidth-latency trade-off and motion blur in low-light, high-speed scenarios. These limitations complicate the tracking process, affecting both the efficiency and accuracy of feature tracking under rapid movements. Event cameras, inspired by biological vision mechanisms, offer a promising alternative due to their high temporal resolution and dynamic range, coupled with low power consumption. In this blog, we aim to reproduce the results in the paper by introduces a novel data-driven feature tracker for event cameras that combines the strengths of event cameras with traditional frames to enhance tracking accuracy and efficiency. The focus of this paper will be directed towards the 

## Network architecture

### Joint Encoder + Feature Network (x2 Patch Encoder)
| Layer | Spatial Size |
|-------|--------------|
| 2x Conv2D 1x1x32 | 31x31 |
| 2x Conv2D 5x5x64 | 23x23 |
| 2x Conv2D 5x5x128 | 15x15 |
| 2x Conv2D 3x3x256 | 5x5 |
| 2x Conv2D 1x1x384 | 1x1 |
| Up + Conv2D 1x1x384 | 5x5 |
| Conv2D 3x3x384 | 5x5 |
| Up + Conv2D 1x1x384 | 15x15 |
| Conv2D 3x3x384 | 15x15 |
| Up + Conv2D 1x1x384 | 23x23 |
| Conv2D 3x3x384 | 23x23 |
| Up + Conv2D 1x1x384 | 31x31 |
| Conv2D 3x3x384 | 31x31 |
| 2x Conv2D 3x3x384 | 31x31 |
| Correlation Layer | 31x31 |
| 2x Conv2D 3x3x128 | 31x31 |
| 2x Conv2D 3x3x64 | 15x15 |
| 2x Conv2D 3x3x128 | 7x7 |
| ConvLSTM 3x3x128 | 7x7 |
| 2x Conv2D 3x3x256 | 3x3 |
| Conv2D 3x3x256 | 1x1 |

### Frame Attention Module
| Layer | Spatial Size |
|-------|--------------|
| Linear 256 | 1x1 |
| Linear 256 | 1x1 |
| MultiHead Attention | 1x1 |
| LayerScale 256 | 1x1 |
| Linear Gating 256 | 1x1 |
| Linear 2 | 1x1 |

The activation layers that are used are mostly Leaky ReLU's. The Softmax and ReLU are also used inside the network setup. 


## Pretrained Weights
Since the training of this model in the original paper is done on the Multiflow Dataset which has a total size of 1.48TB, the authors of the paper have given the weights of those models trained on both the MultiFlow and the EC dataset. The network as such is tested and retrained solely on data derived from the EC dataset. 

## Goal of reproduction
In this reproduction, the goal is to verify the working and the network architecture that is used including the method of training and. The working of the architecture is compared agains their reported results.

## Experiments and tests

### Reproduction of paper results

### Testing different activation layers

### Hyperparameter testing or augmentation

### Verifying usefulness of template component

## Results and Conclusion







