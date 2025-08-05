# Jetson_HTP
## Project Overview
A project based on Nvidia Jetson that integrates multi-source data such as drawings and facial expressions to achieve HTP drawing psychological analysis.
## Memorandum of Understanding
This project is sponsored by the National Natural Science Foundation of China (NSFC) General Project “Research on Interpretable Painting Psychological Analysis Based on Structure-Guided Multimodal Knowledge Graphs” (Project Number: 62372468). For confidentiality reasons, this repository will only include content that does not involve the core elements of the project or personal privacy.  
该项目由中国国家自然科学基金委面上项目“基于结构引导多模态知识图谱的可解释绘画心理分析研究”（项目编号：62372468）赞助，出于保密原则，该repository只会包含不涉及项目核心要素和个人隐私的部分。  
A complete system image may be provided later. You can use an M.2 hard drive reader to burn the image to your solid state drive (256GB hard drive).  
后续可能会提供完整的系统镜像，您可以使用M.2硬盘读取器将镜像烧录至您的固态硬盘（硬盘容量为256GB）
## About flashing Jetson
Currently, I am using Jetson Orin Nano hardware, which has average performance. However, I have flashed it with Super Mode firmware. After testing, I found that Jetson Orin Nano with Super Mode firmware can run multi-modal large model Docker while performing multi-channel data collection tasks, which is difficult to achieve with older firmware (such as Jetpack 6.1). Therefore, I personally recommend that users of older Jetson Orin models flash the new firmware, regardless of whether you need to run the same tasks as I do.  
目前我使用的硬件是Jetson orin nano，性能一般，但是我为他烧写了Super模式固件，经过实验，烧写了super固件的Jetson orin nano能够实现运行多模态大模型docker的同时进行多路数据采集任务，这在旧固件（例如Jetpack6.1）上是很难的，所以我个人推荐目前持有Jetson orin旧机型的朋友刷写新的固件，无论你是否需要运行和我相同的任务。
### Details of the firmware flashing process
My Jetson kit uses an M.2 solid-state drive for storage. I strongly recommend using the SDK manager image burning tool provided by Nvidia to burn the initial image. After installing the SDK manager, simply locate the .conf file containing the word “super” in the `nvidia/nvidia_sdk/XXX_Linux_for_Tegra` directory on the Linux host computer, and then run the following command in that directory.  
```bash
sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 -c tools/kernel_flash/flash_l4t_t234_nvme.xml -p "-c  bootloader/generic/cfg/flash_t234_qspi.xml" --showlogs --network usb0 jetson-orin-nano-devkit-super internal
```
我的jetson套件使用一块M.2固态硬盘作为储存，我强烈建议使用Nvidia官方提供的SDK manager镜像烧录工具进行初始镜像的烧录，完成SDK manager的安装后，只需要在Linux上位机的`nvidia/nvidia_sdk/XXX_Linux_for_Tegra`目录下找到包含super字样的.conf文件，然后在该目录下运行。  
```bash
sudo ./tools/kernel_flash/l4t_initrd_flash.sh --external-device nvme0n1p1 -c tools/kernel_flash/flash_l4t_t234_nvme.xml -p "-c  bootloader/generic/cfg/flash_t234_qspi.xml" --showlogs --network usb0 jetson-orin-nano-devkit-super internal
```
You will then notice that the command line window begins to display the burning progress and return check information. If you have used the SDK manager before, you will find many similarities in the process. Please note that this method does not support parallel installation of other compatible toolkits (such as opencv and pytorch). You may need to manually install these tools after powering on the device.  
之后你会发现在命令行窗口中开始显示烧录的进度和返回的check信息，如果你使用过SDK manager，你会发现很多过程上的相似性，需要注意的是，该方法不支持并行安装兼容的其他工具包（例如opencv和pytorch），您可能需要在上电开机后手动安装这些工具。
## Installing jtop
jtop is a system monitoring tool for NVIDIA Jetson devices, similar to htop or nvidia-smi, but optimized for the Jetson platform. It can display real-time information such as CPU/GPU usage, memory usage, temperature, power consumption, JetPack version, etc., making it ideal for developers to debug and optimize the performance of Jetson devices.  
jtop是一个用于 ​​NVIDIA Jetson​​ 设备的系统监控工具，类似于 htop或 nvidia-smi，但专为 Jetson 平台优化。它可以实时显示 ​​CPU/GPU 使用率​​、​​内存占用​​、​​温度​​、​​功耗​​、​​JetPack 版本​​等信息，非常适合开发者调试和优化 Jetson 设备性能。  
You can use
```bash
sudo pip install jetson-stats
```
to install jtop, then enter
```bash
jtop
```
in the terminal to run jtop.  
你可以使用
```bash
sudo pip install jetson-stats
```
来安装jtop，随后在终端中输入
```bash
jtop
```
就可以运行jtop。
## Compiling and installing OpenCV
At this point, we have completed the flashing of the super mode firmware. Since the project involves image acquisition, we need to install a compatible opencv package. First, uninstall the original opencv package (if already installed).
```bash
sudo apt purge *libopencv*  
sudo apt autoremove  
sudo apt update
```  
此时我们已经完成了带有super模式固件的烧录，由于项目涉及到图像的获取，我们需要安装兼容的opencv包，首先，卸载原装的opencv包（如果已经安装的话）
```bash
sudo apt purge *libopencv*  
sudo apt autoremove  
sudo apt update
```
After that, you need to install the libraries required for compilation.
```bash
sudo apt install -y build-essential cmake git libgtk2.0-dev pkg-config \
libavcodec-dev libavformat-dev libswscale-dev libgstreamer1.0-dev \
libgstreamer-plugins-base1.0-dev python3-dev python3-numpy libtbb2 \
libtbb-dev libjpeg-dev libpng-dev libtiff-dev libv4l-dev v4l-utils curl
```  
之后需要安装编译需要的库
```bash
sudo apt install -y build-essential cmake git libgtk2.0-dev pkg-config \
libavcodec-dev libavformat-dev libswscale-dev libgstreamer1.0-dev \
libgstreamer-plugins-base1.0-dev python3-dev python3-numpy libtbb2 \
libtbb-dev libjpeg-dev libpng-dev libtiff-dev libv4l-dev v4l-utils curl
```
