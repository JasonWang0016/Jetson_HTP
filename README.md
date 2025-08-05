# Jetson_HTP
## Project Overview
A project based on Nvidia Jetson that integrates multi-source data such as drawings and facial expressions to achieve HTP drawing psychological analysis.
## Memorandum of Understanding
This project is sponsored by the National Natural Science Foundation of China (NSFC) General Project “Research on Interpretable Painting Psychological Analysis Based on Structure-Guided Multimodal Knowledge Graphs” (Project Number: 62372468). For confidentiality reasons, this repository will only include content that does not involve the core elements of the project or personal privacy.  
该项目由中国国家自然科学基金委面上项目“基于结构引导多模态知识图谱的可解释绘画心理分析研究”（项目编号：62372468）赞助，出于保密原则，该repository只会包含不涉及项目核心要素和个人隐私的部分。  
A complete system image may be provided later. You can use an M.2 hard drive reader to burn the image to your solid state drive (I used a 256GB hard drive).  
后续可能会提供完整的系统镜像，您可以使用M.2硬盘读取器将镜像烧录至您的固态硬盘（我使用的硬盘容量为256GB）
## About flashing Jetson
Currently, I am using the Jetson Orin Nano hardware, which has average performance. However, I have flashed it with the Super Mode firmware. Through experimentation, I found that the Jetson Orin Nano with the Super firmware can run multi-modal large model Docker while performing data collection tasks, which is difficult to achieve with older firmware (e.g., Jetpack 6.1). Therefore, I personally recommend that users of older Jetson Orin models flash the new firmware, regardless of whether you need to run the same tasks as I do.  
目前我使用的硬件是Jetson orin nano，性能一般，但是我为他烧写了Super模式固件，经过实验，烧写了super固件的Jetson orin nano能够实现运行多模态大模型docker的同时进行数据采集任务，这在旧固件（例如Jetpack6.1）上是很难的，所以我个人推荐目前持有Jetson orin旧机型的朋友刷写新的固件，无论你是否需要运行和我相同的任务。
