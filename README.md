# Wrapper for a clean build of aihabitat.org
contains fresh (march-2020) clone of aiHabitat.
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


#### habitat installation 
 Simplified version, see official install instructions for details.
 Tested on fresh install of Ubuntu 18.04LTS with CUDA enabled graphics card
```sh
sudo apt-get update || true
# These are fairly ubiquitous packages and your system likely has them already,
# but if not, let's get the essentials for EGL support:
sudo apt-get install -y --no-install-recommends \
     libjpeg-dev libglm-dev libgl1-mesa-glx libegl1-mesa-dev mesa-utils xorg-dev freeglut3-dev
     
cd habitat-sim
#this should be already satisfied
pip install -r requirements.txt
python setup.py install 

cd ../habitat-api
#this should be already satisfied
pip install -r requirements.txt
pip install -e .
```


