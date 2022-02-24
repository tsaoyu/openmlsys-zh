## 概述

模型完成训练后，需要将模型及参数持久化成文件，不同的训练框架导出的模型文件中存储的数据结构不同，这给模型的推理系统带来了不便。推理系统为了支持不同的训练框架的模型，需要将模型文件中的数据转换成统一的数据结构。此外，在训练模型转换成推理模型的过程中，需要进行一些如算子融合、常量折叠等模型的优化以提升推理的性能。

推理模型部署到不同的场景，需要满足不同的硬件设备的限制，例如，在具有强大算力的计算中心或数据中心的服务器上可以部署大规模的模型，而在边缘侧服务器、个人电脑以及智能手机上算力和内存则相对有限，部署的模型的规模就相应地要降低。在超低功耗的微控制器上，则只能部署非常简单的机器学习模型。此外，不同硬件对于不同数据类型（如FP32、FP16、BF16、INT8等）的支持程度也不相同。为了满足这些硬件的限制，在有些场景下需要对训练好的模型进行压缩，降低模型的复杂度或者数据的精度，减少模型的参数，以适应硬件的限制。

模型部署到运行环境中执行推理，推理的时延、内存占用、功耗等是影响用户使用的关键因素，优化模型推理的方式有两种，一是设计专有的机器学习的芯片，相对于通用的计算芯片，这些专有芯片一般在能效比上具有很大的优势。二是通过软硬协同最大程度地发挥硬件的能力。对于第二种方式，以CPU为例，如何切分数据块以满足cache大小，如何对数据进行重排以便计算时可以连续访问，如何减少计算时的数据依赖以提升硬件流水线的并行，如何使用扩展指令集以提升计算性能，这些都需要针对不同的CPU架构进行设计和优化。

对于一个企业来讲，模型是属于重要的资产，因此，在模型部署到运行环境以后，保护模型的安全至关重要。本章节会介绍如模型混淆等一些常见的机器学习模型的安全保护手段。

- **模型压缩**

    通过量化、剪枝等手段减小模型体积以及计算复杂度的技术，可以分为需要重训的压缩技术和不需要重训的压缩技术两类。

- **算子融合**

    通过表达式简化、属性融合等方式将多个算子合并为一个算子的技术，融合可以降低模型的计算复杂度及模型的体积。

- **常量折叠**

    将符合条件的算子在离线阶段提前完成前向计算，从而降低模型的计算复杂度和模型的体积。常量折叠的条件是算子的所有输入在离线阶段均为常量。

- **数据排布**

    根据后端算子库支持程度和硬件限制，搜索网络中每层的最优数据排布格式，并进行数据重排或者插入数据重排算子，从而降低部署时的推理时延。

- **模型混淆**

    xxx。