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
virtualenv env
source env/bin/activate
pip install jupyterlab

# Set configuration (password)
jupyter notebook --generate-config
jupyter notebook password
jupyter-lab --ip 0.0.0.0 --port 8889 
```

## Git configuration notes

```
git checkout -b develop
git config --global user.name "visiont3lab"
git config --global user.email "visiont3lab@gmail.com"
git push --set-upstream origin develop
```

## Add script to automaticall start 

```
# https://www.shubhamdipt.com/blog/how-to-create-a-systemd-service-in-linux/
cd cd /etc/systemd/system
sudo vim jupyterlab.service

# write inside 
[Unit]
Description=Jupyterlab development server

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/clara-train-examples
ExecStart=/home/ubuntu/clara-train-examples/startup.sh
Restart=always

[Install]
WantedBy=multi-user.target

sudo systemctl daemon-reload
sudo systemctl start jupyterlab.service
sudo systemctl enable jupyterlab.service
```
