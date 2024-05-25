

![image](https://github.com/Karthikkkunal/PyTorch/assets/150672582/ee788d4a-cbb6-4cec-8b9b-242e672be827)








# PyTorch

PyTorch is a popular framework for building and training neural networks. It offers a dynamic computational graph, which can adapt to various input shapes and sizes across multiple calls, making it ideal for tasks such as image classification with vastly different image dimensions  . Developed by Meta in 2016 on top of the Lua-based Torch package, PyTorch has significantly grown in popularity due to its simplicity in building and training neural networks efficiently  .

# Overview of PyTorch:

PyTorch provides a flexible way to build and train neural networks efficiently. It's particularly well-suited for tasks like image classification, where the input sizes can significantly vary 1 2 .
Dynamic Computational Graph:

Unlike other frameworks, PyTorch's dynamic computational graph allows it to adapt to any compatible input shape across multiple calls. This is especially advantageous for tasks that involve varied input sizes, such as processing images of different resolutions 1 .
Training Neural Networks:

PyTorch simplifies the process of training neural networks by providing a user-friendly interface for building, training, and deploying models. This has made it a popular choice for researchers and industry professionals alike 2 3 .
Image Processing:

Due to its adaptability to various input shapes, PyTorch is highly suitable for image-related tasks like image classification and object detection. Its versatility in handling different input dimensions makes it an ideal choice for tasks involving images of varying sizes 1 .
In conclusion, PyTorch is a powerful and flexible framework for building and training neural networks, offering particular advantages for tasks involving image processing and classification tasks with varying input sizes 

# Installation
Binaries
Commands to install binaries via Conda or pip wheels are on our website: https://pytorch.org/get-started/locally/

# NVIDIA Jetson Platforms
Python wheels for NVIDIA's Jetson Nano, Jetson TX1/TX2, Jetson Xavier NX/AGX, and Jetson AGX Orin are provided here and the L4T container is published here

They require JetPack 4.2 and above, and @dusty-nv and @ptrblck are maintaining them.

From Source
Prerequisites
If you are installing from source, you will need:

Python 3.8 or later (for Linux, Python 3.8.1+ is needed)
A compiler that fully supports C++17, such as clang or gcc (gcc 9.4.0 or newer is required)
We highly recommend installing an Anaconda environment. You will get a high-quality BLAS library (MKL) and you get controlled dependency versions regardless of your Linux distro.

NVIDIA CUDA Support
If you want to compile with CUDA support, select a supported version of CUDA from our support matrix, then install the following:

NVIDIA CUDA
NVIDIA cuDNN v8.5 or above
Compiler compatible with CUDA
Note: You could refer to the cuDNN Support Matrix for cuDNN versions with the various supported CUDA, CUDA driver and NVIDIA hardware

If you want to disable CUDA support, export the environment variable USE_CUDA=0. Other potentially useful environment variables may be found in setup.py.

If you are building for NVIDIA's Jetson platforms (Jetson Nano, TX1, TX2, AGX Xavier), Instructions to install PyTorch for Jetson Nano are available here

AMD ROCm Support
If you want to compile with ROCm support, install

AMD ROCm 4.0 and above installation
ROCm is currently supported only for Linux systems.
If you want to disable ROCm support, export the environment variable USE_ROCM=0. Other potentially useful environment variables may be found in setup.py.

Intel GPU Support
If you want to compile with Intel GPU support, follow these

PyTorch Prerequisites for Intel GPUs instructions.
Intel GPU is currently supported only for Linux systems.
If you want to disable Intel GPU support, export the environment variable USE_XPU=0. Other potentially useful environment variables may be found in setup.py.

Install Dependencies
Common

conda install cmake ninja
# Run this command from the PyTorch directory after cloning the source code using the “Get the PyTorch Source“ section below
pip install -r requirements.txt
On Linux

conda install intel::mkl-static intel::mkl-include
# CUDA only: Add LAPACK support for the GPU if needed
conda install -c pytorch magma-cuda110  # or the magma-cuda* that matches your CUDA version from https://anaconda.org/pytorch/repo

# (optional) If using torch.compile with inductor/triton, install the matching version of triton
# Run from the pytorch directory after cloning
make triton
# On MacOS

# Add this package on intel x86 processor machines only
conda install intel::mkl-static intel::mkl-include
# Add these packages if torch.distributed is needed
conda install pkg-config libuv
# On Windows

conda install intel::mkl-static intel::mkl-include
# Add these packages if torch.distributed is needed.
# Distributed package support on Windows is a prototype feature and is subject to changes.
conda install -c conda-forge libuv=1.39
Get the PyTorch Source
git clone --recursive https://github.com/pytorch/pytorch
cd pytorch
# if you are updating an existing checkout
git submodule sync
git submodule update --init --recursive
Install PyTorch
# On Linux

If you would like to compile PyTorch with new C++ ABI enabled, then first run this command:

export _GLIBCXX_USE_CXX11_ABI=1
If you're compiling for AMD ROCm then first run this command:

# Only run this if you're compiling for ROCm
python tools/amd_build/build_amd.py
Install PyTorch

export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
python setup.py develop
Aside: If you are using Anaconda, you may experience an error caused by the linker:

build/temp.linux-x86_64-3.7/torch/csrc/stub.o: file not recognized: file format not recognized
collect2: error: ld returned 1 exit status
error: command 'g++' failed with exit status 1
This is caused by ld from the Conda environment shadowing the system ld. You should use a newer version of Python that fixes this issue. The recommended Python version is 3.8.1+.

# On macOS

python3 setup.py develop
# On Windows

Choose Correct Visual Studio Version.

PyTorch CI uses Visual C++ BuildTools, which come with Visual Studio Enterprise, Professional, or Community Editions. You can also install the build tools from https://visualstudio.microsoft.com/visual-cpp-build-tools/. The build tools do not come with Visual Studio Code by default.

If you want to build legacy python code, please refer to Building on legacy code and CUDA

CPU-only builds

In this mode PyTorch computations will run on your CPU, not your GPU

conda activate
python setup.py develop
Note on OpenMP: The desired OpenMP implementation is Intel OpenMP (iomp). In order to link against iomp, you'll need to manually download the library and set up the building environment by tweaking CMAKE_INCLUDE_PATH and LIB. The instruction here is an example for setting up both MKL and Intel OpenMP. Without these configurations for CMake, Microsoft Visual C OpenMP runtime (vcomp) will be used.

CUDA based build

In this mode PyTorch computations will leverage your GPU via CUDA for faster number crunching

NVTX is needed to build Pytorch with CUDA. NVTX is a part of CUDA distributive, where it is called "Nsight Compute". To install it onto an already installed CUDA run CUDA installation once again and check the corresponding checkbox. Make sure that CUDA with Nsight Compute is installed after Visual Studio.

Currently, VS 2017 / 2019, and Ninja are supported as the generator of CMake. If ninja.exe is detected in PATH, then Ninja will be used as the default generator, otherwise, it will use VS 2017 / 2019.
If Ninja is selected as the generator, the latest MSVC will get selected as the underlying toolchain.

Additional libraries such as Magma, oneDNN, a.k.a. MKLDNN or DNNL, and Sccache are often needed. Please refer to the installation-helper to install them.

You can refer to the build_pytorch.bat script for some other environment variables configurations

cmd

:: Set the environment variables after you have downloaded and unzipped the mkl package,
:: else CMake would throw an error as `Could NOT find OpenMP`.
set CMAKE_INCLUDE_PATH={Your directory}\mkl\include
set LIB={Your directory}\mkl\lib;%LIB%

:: Read the content in the previous section carefully before you proceed.
:: [Optional] If you want to override the underlying toolset used by Ninja and Visual Studio with CUDA, please run the following script block.
:: "Visual Studio 2019 Developer Command Prompt" will be run automatically.
:: Make sure you have CMake >= 3.12 before you do this when you use the Visual Studio generator.
set CMAKE_GENERATOR_TOOLSET_VERSION=14.27
set DISTUTILS_USE_SDK=1
for /f "usebackq tokens=*" %i in (`"%ProgramFiles(x86)%\Microsoft Visual Studio\Installer\vswhere.exe" -version [15^,17^) -products * -latest -property installationPath`) do call "%i\VC\Auxiliary\Build\vcvarsall.bat" x64 -vcvars_ver=%CMAKE_GENERATOR_TOOLSET_VERSION%

:: [Optional] If you want to override the CUDA host compiler
set CUDAHOSTCXX=C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.27.29110\bin\HostX64\x64\cl.exe

python setup.py develop
Adjust Build Options (Optional)
You can adjust the configuration of cmake variables optionally (without building first), by doing the following. For example, adjusting the pre-detected directories for CuDNN or BLAS can be done with such a step.

# On Linux

export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
python setup.py build --cmake-only
ccmake build  # or cmake-gui build
# On macOS

export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py build --cmake-only
ccmake build  # or cmake-gui build
# Docker Image
Using pre-built images
You can also pull a pre-built docker image from Docker Hub and run with docker v19.03+

docker run --gpus all --rm -ti --ipc=host pytorch/pytorch:latest
Please note that PyTorch uses shared memory to share data between processes, so if torch multiprocessing is used (e.g. for multithreaded data loaders) the default shared memory segment size that container runs with is not enough, and you should increase shared memory size either with --ipc=host or --shm-size command line options to nvidia-docker run.

Building the image yourself
NOTE: Must be built with a docker version > 18.06

The Dockerfile is supplied to build images with CUDA 11.1 support and cuDNN v8. You can pass PYTHON_VERSION=x.y make variable to specify which Python version is to be used by Miniconda, or leave it unset to use the default.

make -f docker.Makefile
# images are tagged as docker.io/${your_docker_username}/pytorch
You can also pass the CMAKE_VARS="..." environment variable to specify additional CMake variables to be passed to CMake during the build. See setup.py for the list of available variables.

make -f docker.Makefile
Building the Documentation
To build documentation in various formats, you will need Sphinx and the readthedocs theme.

cd docs/
pip install -r requirements.txt
You can then build the documentation by running make <format> from the docs/ folder. Run make to get a list of all available output formats.

If you get a katex error run npm install katex. If it persists, try npm install -g katex

# Note: if you installed nodejs with a different package manager (e.g., conda) then npm will probably install a version of katex that is not compatible with your version of nodejs and doc builds will fail. A combination of versions that is known to work is node@6.13.1 and katex@0.13.18. To install the latter with npm you can run npm install -g katex@0.13.18

Previous Versions
Installation instructions and binaries for previous PyTorch versions may be found on our website.

Getting Started
Three-pointers to get you started:

Tutorials: get you started with understanding and using PyTorch
Examples: easy to understand PyTorch code across all domains
The API Reference
Glossary
Resources
PyTorch.org
PyTorch Tutorials
PyTorch Examples
PyTorch Models
Intro to Deep Learning with PyTorch from Udacity
Intro to Machine Learning with PyTorch from Udacity
Deep Neural Networks with PyTorch from Coursera
PyTorch Twitter
PyTorch Blog
PyTorch YouTube
Communication
Forums: Discuss implementations, research, etc. https://discuss.pytorch.org
GitHub Issues: Bug reports, feature requests, install issues, RFCs, thoughts, etc.
Slack: The PyTorch Slack hosts a primary audience of moderate to experienced PyTorch users and developers for general chat, online discussions, collaboration, etc. If you are a beginner looking for help, the primary medium is PyTorch Forums. If you need a slack invite, please fill this form: https://goo.gl/forms/PP1AGvNHpSaJP8to1
Newsletter: No-noise, a one-way email newsletter with important announcements about PyTorch. You can sign-up here: https://eepurl.com/cbG0rv
Facebook Page: Important announcements about PyTorch. https://www.facebook.com/pytorch
For brand guidelines, please visit our website at pytorch.org
Releases and Contributing
Typically, PyTorch has three minor releases a year. Please let us know if you encounter a bug by filing an issue.

We appreciate all contributions. If you are planning to contribute back bug-fixes, please do so without any further discussion.

If you plan to contribute new features, utility functions, or extensions to the core, please first open an issue and discuss the feature with us. Sending a PR without discussion might end up resulting in a rejected PR because we might be taking the core in a different direction than you might be aware of.

To learn more about making a contribution to Pytorch, please see our Contribution page. For more information about PyTorch releases, see Release page.

The Team
PyTorch is a community-driven project with several skillful engineers and researchers contributing to it.

PyTorch is currently maintained by Soumith Chintala, Gregory Chanan, Dmytro Dzhulgakov, Edward Yang, and Nikita Shulga with major contributions coming from hundreds of talented individuals in various forms and means. A non-exhaustive but growing list needs to mention: Trevor Killeen, Sasank Chilamkurthy, Sergey Zagoruyko, Adam Lerer, Francisco Massa, Alykhan Tejani, Luca Antiga, Alban Desmaison, Andreas Koepf, James Bradbury, Zeming Lin, Yuandong Tian, Guillaume Lample, Marat Dukhan, Natalia Gimelshein, Christian Sarofeen, Martin Raison, Edward Yang, Zachary Devito.

