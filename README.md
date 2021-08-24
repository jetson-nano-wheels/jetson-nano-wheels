# Jetson Nano wheels

Unofficial wheels for some machine-learning Python libraries, for the Nvidia Jetson Nano.

If you already know what the Jetson Nano and Python wheels are, you can [skip to the downloads](#downloads) or see my [_awesome list_ of similar projects](#awesome-list-of-similar-projects) below.

## What?

The [Nvidia Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit) is a small computer with a [GPU](https://en.wikipedia.org/wiki/Graphics_processing_unit) that is particularly suited to developing and running machine learning (ML), neural networks, and other artificial intelligence (AI) applications.

The Nano comes with [Jetpack](https://developer.nvidia.com/embedded/jetpack), a software developer kit (SDK) that is available on all [Nvidia Jetson products](https://developer.nvidia.com/embedded/develop/hardware). Jetpack includes the [Jetson Linux Driver Package](https://developer.nvidia.com/embedded/linux-tegra) (L4T) which provides fundamental software for the Jetson board including a booloader and Nvidia drivers, and an operating system based on the Linux operating system (kernel 4.9) and [Ubuntu 18.04](https://releases.ubuntu.com/18.04/). The Jetson Nano provides Nvidia's [Compute Unified Device Architecture](https://en.wikipedia.org/wiki/CUDA) (CUDA) which gives programmers a consistent way to produce code that runs rapidly and in parallel, by taking advantage of the GPU's capabilities.

[Python](https://python.org) is a programming language that is very popular with ML/AI developers.

There are many freely-available [Python software packages](https://pypi.org/) that are optimised for ML/AI development. The packages are distributed in a variety of formats, including "[wheels](https://realpython.com/python-wheels/)", which are a [ready-to-use ("built") form](https://packaging.python.org/glossary/#term-built-distribution) of packages that don't require [building](https://pypa-build.readthedocs.io/en/latest/). They contain code that can simply be moved to the correct location on the destination computer. This makes wheels faster to install (and often quicker to download) than other forms of Python packages including plain source code. Wheels also aim for more consistency, helping to ensure that a computer is in a predictable state after they are installed.


## Why?

Unfortunately, the above circumstances produce a complicated set of [inter-related dependencies](https://en.wikipedia.org/wiki/Dependency_hell). Certain libraries require certain versions of Python or certain versions of CUDA; some of these dependencies are incompatible with each other; and so on. In addition, similar inter-dependencies relate to the build environment, i.e. Ubuntu 18.04 with Jetpack and L4T, which in turn impact the Python packaging environment. This forces developers to engage in time-consuming trial-and-error installation of various versions of Python and Ubuntu-related libraries in order to find a working combination. This can take many days.

The wheels in these projects are offered to save developers from this frustration. The aim is to provide a straightforward and rapid way to get started with machine learning on the Jetson Nano with Python.


## Which AI/ML libraries?

For my personal projects, the following combination works well, and is unlikely to change unless there are specific benefits for my work. I simply don't have the time to explore and maintain other combinations.

  - Python 3.6.x and/or Python 3.7.x
  - numpy 1.19.4 (Python 3.6 only)
  - numpy 1.20.3 (Python 3.7 only)
  - pycuda 2021.1
  - pytools 2021.2.8
  - scipy 1.5.4

<!--
  - cusim
  - numba
  - scikit-learn 0.24.2
  - textacy
-->

### Why this combination?

Basically, lots of trial and error. Here are some of the issues and inter-dependencies I encoutered. The following was my experience on my Jetson running a fresh installation of Jetpack 4.6 with L4T 32.6.1. My experience may not be definitive and I'm happy to be corrected.

  - pycuda 2021.1 only works with Python 3.6, not with Python 3.7 or 3.8.
  - Python 3.6 restricts scipy to maximum version 1.5.4.
  - scipy 1.5.4 requires numpy>=1.14.5

But:

  - pycuda 2021.1 installation [specifies versions of Python and numpy](https://github.com/inducer/pycuda/blob/v2021.1/pyproject.toml): under Python 3.6 it expects numpy 1.12.1.
  - Due to the scipy requirement for numpy>=1.14.5, I've addressed this with a [work-around](https://github.com/jetson-nano-wheels/python3.6-pycuda-2021.1/blob/main/init.sh).

Further:

  - pycuda 2021.1 requires pytools 2021.2.8
  - There is [a bug in numpy 1.19.5](https://github.com/numpy/numpy/issues/18131) which can be [worked around](https://forums.developer.nvidia.com/t/cupy-crashes-on-jetson-nano/169103/3), but I decided to stick to numpy 1.19.4 for now.


## Downloads

Visit the page for each project and follow the instructions there:

  - [https://github.com/jetson-nano-wheels/python3.6-blis-0.7.4](https://github.com/jetson-nano-wheels/python3.6-blis-0.7.4#readme)
  - [https://github.com/jetson-nano-wheels/python3.6-numpy-1.19.4](https://github.com/jetson-nano-wheels/python3.6-numpy-1.19.4#readme)
  - [https://github.com/jetson-nano-wheels/python3.6-pycuda-2021.1](https://github.com/jetson-nano-wheels/python3.6-pycuda-2021.1#readme)
  - [https://github.com/jetson-nano-wheels/python3.6-scipy-1.5.4](https://github.com/jetson-nano-wheels/python3.6-scipy-1.5.4#readme)
  - [https://github.com/jetson-nano-wheels/python3.7-numpy-1.20.3](https://github.com/jetson-nano-wheels/python3.7-numpy-1.20.3#readme)


## Awesome list of similar projects

Are awesome lists still a thing? 😎

  - The [Jetson Zoo](https://elinux.org/Jetson_Zoo) by [@dusty-nv](https://github.com/dusty-nv). Plenty of wheels from Dustin, a developer at Nvidia.
  - Loads of torch wheels here: <https://github.com/KumaTea/pytorch-aarch64>
  - [@QEngineering](https://github.com/qengineering) provide wheels for [TensorFlow](https://github.com/Qengineering/TensorFlow-JetsonNano) (and some [community-built add-ons for TF](https://github.com/Qengineering/TensorFlow-Addons-Jetson-Nano)), [Torch](https://github.com/Qengineering/PyTorch-Jetson-Nano), and [Paddle](https://github.com/Qengineering/Paddle-Jetson-Nano). They also provide build instructions for other libraries including [OpenCV](https://github.com/Qengineering/Install-OpenCV-Jetson-Nano).

## Disclaimer

As with many other open-source projects, everything in the [Jetson Nano Wheels](https://github.com/jetson-nano-wheels/) projects are offered "as-is", without warranty of any kind, express or implied. All contributors disclaim any liability for any direct, indirect, incidental, consequential or other damages however caused, arising in any way from, or in connection with, the use of the software or any other dealings in the software. See the [LICENSE](LICENSE) file in each project for further details.

This project is unofficial, and has nothing to do with Nvidia whatsoever.


## What's the logo?

It's a diagram of a [dendrimer](https://en.wikipedia.org/wiki/Dendrimer), a polymer with a highly ordered, branching structure, also known as a _cascade molecule_. It seemed appropriate :smile:
