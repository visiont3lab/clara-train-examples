# Setup instructions

## Setup AWS ubuntu 20.04

```
sudo apt update
sudo apt install nvidia-driver-440
sudo reboot
sudo apt install python3 python3-dev python3-virtualenv
git clone https://github.com/visiont3lab/clara-train-examples.git
cd clara-train-examples
git checkout develop 
```

## Setup  clara-train-sdk4 to run examples

```
# clara-train-sdk info https://docs.nvidia.com/clara/clara-train-sdk
# Working: install docker nvidia-docker kubernets 
cd clara-train-examples/PyTorch/NoteBooks/scripts
chmod a+x installDocker.sh
sudo ./installDocker.sh

# --> Working: start clar-train-notebooks
chmod a+x ./startClaraTrainNoteBooks.sh
chmod a+x ./stopClaraTrainNoteBooks.sh
sudo ./startClaraTrainNoteBooks.sh

# --> Working: Start only notebooks + clara-train
chmod a+x ./startDocker.sh
sudo ./startDocker.sh

# --> Recommended: Working: Run all:
chmod a+x ./startup.sh
sudo ./startup.sh
```

## Add script to automaticall start 

```
# https://www.shubhamdipt.com/blog/how-to-create-a-systemd-service-in-linux/
cd /etc/systemd/system
sudo vim jupyterlab.service

# write inside 
# note: change user <ubuntu> with your current user
[Unit]
Description=Jupyterlab development server

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/clara-train-examples/PyTorch/NoteBooks/scripts/
ExecStart=/home/ubuntu/clara-train-examples/PyTorch/NoteBooks/scripts/startup.sh
Restart=always

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl start jupyterlab.service
sudo systemctl enable jupyterlab.service
```



## Run clara train + ohif + triton

```
# https://www.shubhamdipt.com/blog/how-to-create-a-systemd-service-in-linux/
cd /etc/systemd/system
sudo vim jupyterlab.service

# write inside 
# note: change user <ubuntu> with your current user
[Unit]
Description=Jupyterlab development server

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/clara-train-examples/PyTorch/NoteBooks/AIAA/OHIF-Orthanc
ExecStart=/home/ubuntu/clara-train-examples/PyTorch/NoteBooks/AIAA/OHIF-Orthanc/restart.sh
Restart=always

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl start jupyterlab.service
sudo systemctl enable jupyterlab.service
```