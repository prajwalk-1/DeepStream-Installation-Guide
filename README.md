# DeepStream Installation WSL-Ubuntu-20.04

## Overview

DeepStream is NVIDIA's streaming analytics toolkit that enables high-performance, real-time video analytics. It leverages NVIDIA's powerful hardware and software stack, including TensorRT and CUDA, to process video streams efficiently. DeepStream supports various AI models for tasks such as object detection, classification, tracking, and more.

In this guide, you will learn how to set up DeepStream 6.2 on Windows Subsystem for Linux (WSL) 2 with Ubuntu 20.04. The setup includes CUDA 11.8, cuDNN, and TensorRT 8.6, providing a complete environment for developing and deploying video analytics applications.

## Prerequisites

- **WSL 2**: Ensure you have Windows Subsystem for Linux version 2 installed.
- **Ubuntu 20.04**: You should have Ubuntu 20.04 installed on WSL 2.

### Installing Ubuntu 20.04 on WSL 2

You can install Ubuntu 20.04 from the Microsoft Store or by using a command-line tool.

#### Option 1: Install from Microsoft Store

1. Open the [Microsoft Store](https://www.microsoft.com/store/productId/9N9TNGVNDL3Q).
2. Search for "Ubuntu 20.04".
3. Click "Get" to install Ubuntu 20.04.

#### Option 2: Install Using `wsl` Command

1. Open PowerShell or Command Prompt as Administrator.
2. Install Ubuntu 20.04 using the following command:
   ```bash
   wsl --install -d Ubuntu-20.04
   ```

### Initial Setup

1. **Set Up Username and Password**:
   - After installation, launch Ubuntu 20.04.
   - Follow the prompts to create a username and password.

## Steps

### 1. Update and Upgrade Ubuntu

```bash
sudo apt update
sudo apt upgrade
```

### 2. Install NVIDIA Drivers on Windows

1. **Download and Install NVIDIA Drivers**: 
   - [NVIDIA Drivers for Windows](https://www.nvidia.com/Download/index.aspx)

2. **Verify Installation**:
   - After installing, verify the driver is working by running `nvidia-smi` in the Windows Command Prompt or PowerShell.

### 3. Install CUDA 11.8

1. **Download CUDA 11.8**:
   - [CUDA 11.8 Download Page](https://developer.nvidia.com/cuda-11-8-0-download-archive)

2. **Install CUDA Toolkit**:
   - Download the `.deb` file for Ubuntu 20.04 from the CUDA download page.
   - Install the `.deb` file:
     ```bash
     sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
     sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7fa2af80
     sudo apt-get update
     sudo apt-get install cuda
     ```

3. **Set Up Environment Variables**:
   - Add the following to your `.bashrc` or `.zshrc` file:
     ```bash
     export PATH=/usr/local/cuda-11.8/bin:$PATH
     export LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH
     ```

   - Apply the changes:
     ```bash
     source ~/.bashrc
     ```

4. **Verify CUDA Installation**:
   - Check the CUDA version:
     ```bash
     nvcc --version
     ```

### 4. Install cuDNN

1. **Download cuDNN for CUDA 11.8**:
   - [cuDNN Download Page](https://developer.nvidia.com/rdp/cudnn-download)

2. **Extract and Install cuDNN**:
   - After downloading the `.tgz` file, extract it:
     ```bash
     tar -xzvf cudnn-*-linux-x86_64-v*.tgz
     ```

   - Copy the files to the CUDA directory:
     ```bash
     sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
     sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
     sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
     ```

3. **Verify cuDNN Installation**:
   - Check the cuDNN version:
     ```bash
     dpkg -l | grep libcudnn
     ```

### 5. Install TensorRT 8.6

1. **Download TensorRT 8.6**:
   - [TensorRT Download Page](https://developer.nvidia.com/nvidia-tensorrt-download)

2. **Install TensorRT**:
   - Download the `.deb` files for TensorRT 8.6 (you might need the `libnvinfer`, `libnvinfer-plugin`, and `libnvinfer-dev` packages).
   - Install the packages:
     ```bash
     sudo dpkg -i libnvinfer8_8.6.0-1+cuda11.8_amd64.deb
     sudo dpkg -i libnvinfer-plugin8_8.6.0-1+cuda11.8_amd64.deb
     sudo dpkg -i libnvinfer-dev_8.6.0-1+cuda11.8_amd64.deb
     ```

3. **Verify TensorRT Installation**:
   - Check TensorRT version:
     ```bash
     dpkg -l | grep nvidia-tensorrt
     ```

### 6. Install DeepStream 6.2

1. **Download DeepStream 6.2**:
   - [DeepStream 6.2 Download Page](https://developer.nvidia.com/deepstream-sdk-download)

2. **Install DeepStream**:
   - Download the `.deb` file and install it:
     ```bash
     sudo dpkg -i deepstream-6.2_*.deb
     ```

3. **Set Up DeepStream Environment Variables**:
   - Add the following to your `.bashrc` or `.zshrc` file:
     ```bash
     export PATH=/usr/local/deepstream/deepstream-6.2/bin:$PATH
     export LD_LIBRARY_PATH=/usr/local/deepstream/deepstream-6.2/lib:$LD_LIBRARY_PATH
     ```

   - Apply the changes:
     ```bash
     source ~/.bashrc
     ```

4. **Verify DeepStream Installation**:
   - Run a sample DeepStream application to ensure it works:
     ```bash
     deepstream-app
     ```

### 7. Troubleshooting

- **Verify CUDA Installation**:
  If you encounter issues, ensure that the CUDA paths are correctly set and that the NVIDIA drivers are correctly installed on Windows.

- **Check Compatibility**:
  Ensure that the versions of CUDA, cuDNN, TensorRT, and DeepStream are compatible with each other.

- **Review Logs**:
  Look at the log files for DeepStream and TensorRT for detailed error messages.

## Additional Resources

- [NVIDIA DeepStream Documentation](https://docs.nvidia.com/metropolis/deepstream/dev-guide/)
- [NVIDIA CUDA Documentation](https://docs.nvidia.com/cuda/)
- [NVIDIA cuDNN Documentation](https://docs.nvidia.com/deeplearning/cudnn/)
- [NVIDIA TensorRT Documentation](https://docs.nvidia.com/deeplearning/tensorrt/)


<html>
<body>
    <div class="container">
        <h2><span class="emoji">⚠️</span> Need Help?</h2>
        <p>If you encounter any errors or need assistance, please don't hesitate to reach out:</p>
        <p><a href="mailto:kanadeprajwal24@gmail.com" class="email">kanadeprajwal24@gmail.com</a></p>
    </div>
</body>
</html>
