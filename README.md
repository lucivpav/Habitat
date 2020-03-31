# Wrapper for a clean build of aihabitat.org
contains fresh (march-2020) clone of aiHabitat.

```sh
git clone git@gitlab.ciirc.cvut.cz:steidsta/aag-habitat.git --recurse-submodules
```
## demo:
```sh
cd habitat-api
    
python /examples/tutorial_example.py 
```
This should open up a window with the simulation. Move around with WAD keys. Press F to close.

## install
set up  and activate the conda environment specified in *.yml file
#### Conda environment requires python 3.6 + one of { Anaconda3 , Miniconda3}
```sh
conda env create -f conda_env_habitat.yml
```
if instalatin for some reason fails, part of environment will be probably already created. to continue use 
```sh
conda env update -f conda_env_habitat.yml
```

#### habitat installation - Work in progress version, some steps might be ambiguous
 Simplified version, see official install instructions for details.
 Tested on fresh install of virtualBox Ubuntu 18.04LTS 4GB RAM
```sh
sudo apt-get update || true
# These are fairly ubiquitous packages and your system likely has them already,
# but if not, let's get the essentials for EGL support:
sudo apt-get install -y --no-install-recommends \
     libjpeg-dev libglm-dev libgl1-mesa-glx libegl1-mesa-dev mesa-utils xorg-dev freeglut3-dev
     
sudo apt install gcc
sudo apt-get update && sudo apt-get install build-essential

cd habitat-api
#this should be already satisfied
pip install -r requirements.txt
pip install -e .

cd ../habitat-sim
#this should be already satisfied
pip install -r requirements.txt
#to avoid memory issues
python setup.py build_ext --parallel 1 install
python setup.py install 
```
if instalation for some reason fails, it might happen that build is corrupted, in order to avoid potential issues (e.g. missing build/dependencies.json), delete build folder

to quickly verify the instalation once can open python and check whether the modules are available
```sh
$python
>>> import habitat
>>> import habitat_sim

...
>>>exit()
```


