# Jetson_HTP
## Project Overview
A project based on Nvidia Jetson that integrates multi-source data such as drawings and facial expressions to achieve HTP drawing psychological analysis.
## Memorandum of Understanding
This project is sponsored by the National Natural Science Foundation of China (NSFC) General Project “Research on Interpretable Painting Psychological Analysis Based on Structure-Guided Multimodal Knowledge Graphs” (Project Number: 62372468). For confidentiality reasons, this repository will only include content that does not involve the core elements of the project or personal privacy.  
该项目由中国国家自然科学基金委面上项目“基于结构引导多模态知识图谱的可解释绘画心理分析研究”（项目编号：62372468）赞助，出于保密原则，该repository只会包含不涉及项目核心要素和个人隐私的部分。  
A complete system image may be provided later. You can use an M.2 hard drive reader to burn the image to your solid state drive (I used a 256GB hard drive).  
后续可能会提供完整的系统镜像，您可以使用M.2硬盘读取器将镜像烧录至您的固态硬盘（我使用的硬盘容量为256GB）
## About flashing Jetson
Currently, I am using Jetson Orin Nano hardware, which has average performance. However, I have flashed it with Super Mode firmware. After testing, I found that Jetson Orin Nano with Super Mode firmware can run multi-modal large model Docker while performing multi-channel data collection tasks, which is difficult to achieve with older firmware (such as Jetpack 6.1). Therefore, I personally recommend that users of older Jetson Orin models flash the new firmware, regardless of whether you need to run the same tasks as I do.
目前我使用的硬件是Jetson orin nano，性能一般，但是我为他烧写了Super模式固件，经过实验，烧写了super固件的Jetson orin nano能够实现运行多模态大模型docker的同时进行多路数据采集任务，这在旧固件（例如Jetpack6.1）上是很难的，所以我个人推荐目前持有Jetson orin旧机型的朋友刷写新的固件，无论你是否需要运行和我相同的任务。
### Details of the firmware flashing process
我的jetson套件使用一块M.2固态硬盘作为储存，我强烈建议使用Nvidia官方提供的SDK manager镜像烧录工具进行初始镜像的烧录，完成SDK manager的安装后，只需要在Linux上位机的`nvidia/nvidia_sdk/XXX_Linux_for_Tegra`目录下找到包含super字样的.conf文件，然后在该目录下运行。  
'''bash
sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 -c tools/kernel_flash/flash_l4t_t234_nvme.xml -p "-c  bootloader/generic/cfg/flash_t234_qspi.xml" --showlogs --network usb0 jetson-orin-nano-devkit-super internal
'''  
My Jetson kit uses an M.2 solid-state drive for storage. I strongly recommend using the SDK manager image burning tool provided by Nvidia to burn the initial image. After installing the SDK manager, simply locate the .conf file containing the word “super” in the `nvidia/nvidia_sdk/XXX_Linux_for_Tegra` directory on the Linux host computer, and then run the following command in that directory.  
'sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 -c tools/kernel_flash/flash_l4t_t234_nvme.xml -p “-c  bootloader/generic/cfg/flash_t234_qspi.xml” --showlogs --network usb0 jetson-orin-nano-devkit-super internal'
