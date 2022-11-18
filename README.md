# Performance-modeling-of-CNN-accelerators

Our project proposes the implementation of the Convolutional loop of  Neural Networks, as well as several performance enhancement methods such as unrolling and tiling. The large design space of the accelerator makes it impractical to search for the optimal design in the implementation phase. To address this problem, a performance model is described to estimate the performance and resource utilization of an FPGA implementation. We are executing our codebase on the PYNQ-Z2 board, which is an FPGA-based development board based on the ZYNQ XC7Z020, and drawing conclusions based on observations from CPU, execution time,  swap memory, and disc space usage of various strategies. All of the other models are outperformed by the model that includes both unrolling and tiling CNN.

## Overview of Convolution Operation:
The basic function of CNN algorithms is to add the products of pixel values (e.g., features, activations, or neurons) and kernel weights along various dimensions of the kernel and feature maps.

![Convolution Loop](https://user-images.githubusercontent.com/75046231/202720324-d3f63968-316c-412b-88bb-3ce98af60283.png) ![Unrolling + Tiling](https://user-images.githubusercontent.com/75046231/202720339-40b7d00f-c204-4922-b143-7de949ef74f7.png)
![Convolution Operation](https://user-images.githubusercontent.com/75046231/202720334-c19ccdf5-f521-4d71-baac-59f59e038689.png)

The above equation shows the convolution loop operation on a 2D image input matrix where, 
			      S = sliding stride
            L= number of convolution layer
            (x,y) = position of pixel in 2D input matrix
            weight() = kernel matrix with weight



## Convolution Loop Optimization:
Loop optimization techniques, e.g., unrolling and tilling, are employed to customize the computation and communication patterns in a CNN accelerator.

### Unrolling :
The parallel computation is directed along multiple convolution dimensions via loop unrolling.
These factors determine the number of Processing Engines(PEs) , which determines the number of Digital Signal Processings(DSPs)required in the FPGA to implement PEs, and therefore the computing latency.
The origin kernel computes 1 element at a time and it will be executed Nx3x3 times; With pragma unroll, the kernel computes 3 elements at the same time so that it only takes Nx3 iterations.

### Tiling :
To promote data locality, loop tilling breaks a big CNN layer into numerous little tiles that can be supported by on-chip buffers.
The needed buffer capacity is controlled by tiling factors, which also impact DRAM access and consequently DRAM transaction latency.
Multithreading was used to implement all the tiles together after breaking the image into tiles and treating computation of each tile as a thread.

Name of the model  | CPU Usage (%) | Execution Time(sec) 
------------- | ------------- | -------------
CNN  | 53.7  | 201.251
CNN with Tiling  | 96.1  | 162.766
CNN with Unrolling  | 52.3  | 138.128
CNN with (Unrolling+Tiling)  | 94.2  | 153.935


