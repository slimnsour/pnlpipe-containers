![](docs/pnl-bwh-hms.png)

[![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.2584271.svg)](https://doi.org/10.5281/zenodo.2584271) [![Python](https://img.shields.io/badge/Python-3.6-green.svg)]() [![Platform](https://img.shields.io/badge/Platform-linux--64%20%7C%20osx--64%20%7C%20win--64-orange.svg)]()

Developed by Tashrif Billah and Sylvain Bouix, Brigham and Women's Hospital (Harvard Medical School).


Table of Contents
=================

   * [pnlpipe containers](#pnlpipe-containers)
   * [Citation](#citation)
   * [Tests](#tests)
      * [Nominal test](#nominal-test)
      * [Detailed test](#detailed-test)
   * [Data analysis](#data-analysis)

Table of Contents created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)


# pnlpipe containers

The *pnlpipe* docker container is publicly hosted at [https://cloud.docker.com/u/tbillah/repository/docker/tbillah/pnlpipe](https://cloud.docker.com/u/tbillah/repository/docker/tbillah/pnlpipe)


This repository provides recipes for building [*pnlpipe* software](https://github.com/pnlbwh/pnlpipe_software) containers.
The containers contain the following software:

* python3
* ANTs
* BRAINSTools
* UKFTractography
* tract_querier
* dcm2niix
* trainingDataT1AHCC
* trainingDataT2Masks


*pnlpipe* pipeline depends on two other software, installation of which requires you to agree to their license terms:

* [FreeSurfer](https://surfer.nmr.mgh.harvard.edu/fswiki/DownloadAndInstall)
* [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation)

You should download and install them directly from their websites and then run *pnlpipe* as follows:

> docker run --rm -ti -v /host/path/to/freesurfer:/home/pnlbwh/freesurfer -v /host/path/to/fsl:/home/pnlbwh/fsl tbillah/pnlpipe

In the above, `/host/path/to/` is where you install the software and the host software are mounted on the container `tbillah/pnlpipe`. 
When you run the container like above, it will give you a shell with all of the above software.


**NOTE** *FreeSurfer* and *FSL* are assumed to be mounted on the container interactive shell (`-ti` flag). 
So make sure to install them on your host machine and mount them before launching the interactive shell.


# Citation

If *pipeline* container is useful in your research, please cite as below:

Billah, Tashrif*; Eckbo, Ryan*; Bouix, Sylvain; Norton, Isaiah; Processing pipeline for anatomical and diffusion weighted images, 
https://github.com/pnlbwh/pnlpipe, 2018, DOI: 10.5281/zenodo.2584271

# Tests

## Nominal test
Once inside the container, you can test its functionality with:

> atlas.py --help

> UKFTractography --help

> DWIConvert --help


The above should print corresponding help messages without any error.

## Detailed test
Additionally, you can run *pnlpipe* test https://github.com/pnlbwh/pnlpipe#tests to before doing your data analysis.


You are welcome to read the details of *pnlpipe* at https://github.com/pnlbwh/pnlpipe


# Data analysis

With the above `docker run` command, just mount another directory that contains your data that you would like to analyze using *pnlpipe*:

> docker run --rm -ti -v /host/path/to/freesurfer:/home/pnlbwh/freesurfer -v /host/path/to/fsl:/home/pnlbwh/fsl 
-v /host/path/to/myData:/home/pnlbwh/myData tbillah/pnlpipe

The files you generate at `/home/pnlbwh/myData` are saved at `/host/path/to/myData`.


**NOTE** The container `tbillah/pnlpipe` is not equipped with GUI. So, if you need to visually look at your MRI, 
launch fsleyes, freeview etc from your host machine, not from the container. Since processed data is saved in 
the host directory that you mounted on the container, it shouldn't be a problem to explore them from your host 
machine.

