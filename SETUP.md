# Setup instructions

## Setup AWS ubuntu 20.04

```
sudo apt update
sudo apt install nvidia-driver-440
sudo reboot
sudo apt install python3 python3-dev
git clone https://github.com/visiont3lab/clara-train-examples.git
cd clara-train-examples
git checkout develop 
virtualenv env
source env/bin/activate
pip install jupyterlab
jupyter-lab --ip 0.0.0.0 --port 8889 --NotebookApp.token=''
```
