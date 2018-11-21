# RAPIDS installation for HackTalks workshop

# Any environment

### Requirements

* Docker CE v18+
    * Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/
    * Mac: https://docs.docker.com/docker-for-mac/install/
    * Windows (didn't test): https://docs.docker.com/docker-for-windows/install/

# With NVIDIA GPU

### Requirements

* Ubuntu 16.04+ (didn't test other distros)
* GPU architecture: Pascal or better
* NVIDIA drivers 396+, CUDA 9.2+:
    * https://developer.nvidia.com/cuda-92-download-archive (Ubuntu 16.04)
    * https://developer.nvidia.com/cuda-downloads (Ubuntu 18.04)

    You need to reboot for the change to take effect.
* Docker CE v18+ https://docs.docker.com/install/linux/docker-ce/ubuntu/
* NVIDIA Docker v2+ https://github.com/NVIDIA/nvidia-docker#ubuntu-140416041804-debian-jessiestretch


### Pulling the image and starting it

`docker pull tuomars/hacktalks:rapids_with_e2e` (pulls from Docker Hub)

`docker run --runtime=nvidia -it --rm -p 8888:8888 -p 8787:8787 -p 8786:8786 tuomars/hacktalks:rapids_with_e2e`

If the above doesn't work for some reason, try

`docker pull tuomars/hacktalks:rapids_without_e2e` (pulls from Docker Hub)

`docker run --runtime=nvidia -it --rm -p 8888:8888 tuomars/hacktalks:rapids_without_e2e`

This image doesn't contain Dask support.

### Smoke test

```bash
> python
>>> import cudf
>>> import cuml
```

### Launching a notebook

In the container,

`./start_notebook.sh`

Then, copy-paste the reported URL to your web browser (of the form http://localhost:8888/?token=abc123) and see the folder `/notebooks`.

# Without NVIDIA GPU

You should be able to follow the workshop thanks to cudf and cuml being near drop-in replacements for pandas and
sklearn, respectively.

### Requirements
* Docker CE v18+

### Pulling the image and starting it

`docker pull tuomars/hacktalks:cpu` (pulls from Docker Hub)

`docker run -it --rm -p 8888:8888 tuomars/hacktalks:cpu`

### Smoke test

```bash
> python
>>> import pandas
>>> import sklearn
```

### Launching a notebook

In the container, run

`./start_notebook.sh`

Then, copy-paste the reported URL to your web browser (of the form http://localhost:8888/?token=abc123) and see the folder `/notebooks`.

# Not recommended for this workshop but possible: local installation

If you have an NVIDIA GPU, see: https://github.com/RAPIDSai and install cudf and cuml following the instructions in the repos.

### Requirements

* miniconda/anaconda
* python 3.5+
* pandas (0.20.3)
* scikit-learn
* matplotlib
* notebook

Datasets used in this workshop are available at: https://drive.google.com/file/d/1rdzp7xqtTDbrDaZmreeHfPn81ZacDUtl/view?usp=sharing

Launching a notebook: `ipython notebook`