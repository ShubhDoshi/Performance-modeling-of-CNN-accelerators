# Performance-modeling-of-CNN-accelerators

Our project proposes the implementation of the Convolutional loop of  Neural Networks, as well as several performance enhancement methods such as unrolling and tiling. The large design space of the accelerator makes it impractical to search for the optimal design in the implementation phase. To address this problem, a performance model is described to estimate the performance and resource utilization of an FPGA implementation. We are executing our codebase on the PYNQ-Z2 board, which is an FPGA-based development board based on the ZYNQ XC7Z020, and drawing conclusions based on observations from CPU, execution time,  swap memory, and disc space usage of various strategies. All of the other models are outperformed by the model that includes both unrolling and tiling CNN.

## Overview of Convolution Operation:
The basic function of CNN algorithms is to add the products of pixel values (e.g., features, activations, or neurons) and kernel weights along various dimensions of the kernel and feature maps.

![Convolution Loop](https://user-images.githubusercontent.com/75046231/202720324-d3f63968-316c-412b-88bb-3ce98af60283.png) ![Unrolling + Tiling](https://user-images.githubusercontent.com/75046231/202720339-40b7d00f-c204-4922-b143-7de949ef74f7.png)
![Convolution Operation](https://user-images.githubusercontent.com/75046231/202720334-c19ccdf5-f521-4d71-baac-59f59e038689.png)


