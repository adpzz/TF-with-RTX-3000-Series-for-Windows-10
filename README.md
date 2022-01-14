# Tensorflow with RTX 3000 Series for Windows 10

This is a step-by-step to use the new GPU generations in Windows 10.

There have been several reports for long initialization times for 3000 series GPU with Tensorflow and Keras. Likewise, bad performance both to train and predict models.

We need to take into account that the new NVIDIA GPU generation is based on Ampere architecture, which means CUDA v11.0 and higher is required same for cuDNN v11.0.
On the other hand, is required a Tensorflow version with built with CUDA v11.0 (in this case 2.5, the nightly version). In addition, to keeping updated, grant compatibility and support is recommended the use of Python 3.8+ (tf-nightly version requires Python 3.8+).

I'm using:
- CUDA v11.2
- cuDNN Toolkit v11.2
- Python 3.8.5

Below you will find the step-by-step to get ready with your new GPU:

1. First we do need a Microsoft Visual Studio version for C++ to properly install the other components. You can download a free version of Visual Studio which is the [Visual Studio Community Edition](https://visualstudio.microsoft.com/es/vs/community/). Install the C++ components selecting the "Desktop development with C++" and then the first 6 options. If you already have this done skip this first step.

2. Now you have to download and install the CUDA v11.0+ from NVIDIA which can be found [here](https://developer.nvidia.com/cuda-downloads) (remember to create a developer account if required). Right now it appears v10 (this should download the "cuda_11.2.0_460.89_win10.exe" file which is almost 3GB). Run this .exe file with admin rights using the express installation, but if you already have installed the GeForce Experience, you can choose the Custom Option and select only those packages with higher version than yours.

3. Once installed the VS and the CUDA components, its time to add the cuDNN DLLs and extra files. You can download the cuDNN files from [here](https://developer.nvidia.com/rdp/cudnn-download) (this file is approx 700MB). With the file in your desktop, extract it. Now you will find 3 folders, "lib", "include" and "bin". Copy those 3 folders in the CUDA directory (which should be in ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x`` -the "x" means your current CUDA version-).

3.a. Probably you'll face an error steps ahead related with missing ``cusolver64_10.dll`` file in ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x\bin\`` directory. Quick troubleshooting for this issue is to copy the ``cusolver64_11.dll`` and rename as ``cusolver64_10.dll``. However, if the ``cusolver64_10.dll`` file does exists, you should skip this step.

4. Great! Everything is installed! Its time to set-up the System Variables. Press the Windows Key and search for "Edit the system environment variables". In the "Advanced" tab click on "Environment Variables..." button. Now in the "System Variables" section, find and open the "Path" variable. Here you need to add the following paths:

- ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x\bin``
- ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x\include``
- ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x\libnvvp``
- ``C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\vx.x\extras\CUPTI\lib64``

Note: if the path already exists you don't need to add it again.

5. Time to restart your pc to apply all changes! 😁

6. I strongly recommend the use of [virtual environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) so [Anaconda](https://www.anaconda.com/) is a wonderful option. Once Anaconda is installed, open an Anaconda prompt with admin rights to avoid restrictions during the process and create a new "test" virtual environment. Just type ``conda create -n py38tf python=3.8`` and press enter. Wait till the environment is created (press yes if required).

7. Activate your brand new virtual environment typing ``conda activate py38tf`` and press enter.

8. Now install the nightly tf version with gpu support typing ``pip install tf-nightly-gpu``. Once installed, install the reaming packages. I recommend to install jupyter, pandas, matplotlib and scikit-learn. Just type ``conda install jupyter pandas matplotlib scikit-learn``.

9. Launch Jupyter Notebook and run the file ``GPU_VISIBILITY_TEST.ipynb``. Now you should see all the GPU in your system. Likewise, you can test your GPU over a simple training script from Tensorflow the [Basic classification: Classify images of clothing](https://www.tensorflow.org/tutorials/keras/classification?hl=en-419) - ``train_test.ipynb``.

That's all!
You're ready to rock with your brand new RTX 3000 Series GPU! 😎
