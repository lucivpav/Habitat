# Wrapper for a clean build of aihabitat.org
contains fresh (march-2020) clone of aiHabitat.

```sh
git clone git@github.com:lucivpav/Habitat.git --recurse-submodules
```

## Install
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
 Tested on 
 - fresh install of (dualboot) Ubuntu 18.04LTS 16GB ram (4GB should be sufficient) with cuda enabled gpu
 - Ubuntu 16LTS server
 - virtual box Ubuntu 18.04LTS - installed, however when running there are issues with openGL capability, required GL 4.10, virtalbox provides 2.x. Possible workaround: install as on server (headless) and forward graphics to X11 server on host OS
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
# no errors? good
...
>>>exit()
```


## Demo
 dataset (dl.fbaipublicfiles.com/habitat/habitat-test-scenes.zip) 
Download the test scenes data and extract data folder in zip to habitat-api/data/ where habitat-api/ is the github repository folder.
```sh
cd habitat-api
    
python examples/tutorial_example.py 
```
This should open up a window with the simulation. Move around with WAD keys. Press F to close.    
    
# How to connect to habitat capable server with local X11 server
step 1: connect to ciirc vpn : https://portal.ciirc.cvut.cz/it-issues/internet/vpn-ciirc

step 2: install Xming  on your pc (for graphical output) 

step 3: ssh connect to 10.35.125.131 with flag -X (to enable forwarding, if using putty: at ssh.X11forwarding enable forwarding) 

step 4: install habitat: 
  
*    a] install anaconda
*    b] git clone git@github.com:lucivpav/Habitat.git --recurse-submodules
*    c] create environment and activate
*    d] skip the sudo apt install, as all should be present already
*    e] use flag  --headless for habitat-sim, --parallel 1 is not necessary
*    f] download and unzip to habitata-api/data the test dataset for example: wget dl.fbaipublicfiles.com/habitat/habitat-test-scenes.zip
*    g] cd havitat-api and run python examples/tutorial_example.py 
    
you should see the simulator





