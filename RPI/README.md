# Raspberry PI resources:


* [Servo motor control](/RPI/Python_resources/Motors/Servo_motor_control.ipynb)
* [Ultrasound distance sensing](/RPI/Python_resources/Sensors/ultrasound_distance.ipynb)

You may also be interested in the following communications resources:
* [Bluetooth communications using the Python Socket library (PC/ Raspberry PI)](/Communications/Bluetooth/pc/)
* [TCP/IP communications using the Python Socket library (PC/ Raspberry PI)](/Communications/TCPIP)

# Setting up your Raspberry pi to run these notebooks

If you would like to configure your raspberry pi to use jupyter follow the steps below.

## Initial Setup

I'll assume you have an operating system with a terminal, and that can ssh. On windows, check out the [windows subsystem for linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10), and [putty](https://www.putty.org/). I will be using Ubuntu, which generally ships with terminal and ssh.

I [installed Ubuntu 20.04 server](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview) on my raspberry pi, because I wanted a 64 bit operating system for PyTorch (see below). If you want a graphical user interface, choose Ubuntu Desktop instead of server. As part of these installation instructions, I gave my pi a hostname ENG5105GROUPNO to make it easier to ssh into.

Let's log into our Ubuntu raspberry pi using ssh
```
ssh ubuntu@ip_address
```
Once you're in, it's time to install some useful software. [tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer for running multiple programs in one terminal and remotely executing programs that will continue to run if the network drops. [htop](https://htop.dev/) is a terminal process viewer that will be useful to monitor processor load/ memory use. [vim](https://vim-adventures.com/) is a text editor for people who hate [emacs](https://en.wikipedia.org/wiki/Editor_war). Most of the rest are things we'll use in python. [Minicom](https://en.wikipedia.org/wiki/Minicom#:~:text=Minicom%20is%20a%20text%2Dbased,Telix%20but%20is%20open%20source.) is a text-based terminal useful for serial communication testing.

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git python3-scipy jupyter libatlas-base-dev tmux htop vim python3-pip python3-matplotlib libgl-dev net-tools python3-gpiozero avahi-daemon
```

We installed the avahi daemon to make getting on our pi easier. Assuming you're on the same network and set up the hostname correctly, logging in to the pi remotely will be a lot easier going forward, just using:
```
ssh ubuntu@ENG5105GROUPNO.local
```

Ok, lets continue to install some more packages on the pi.
``` 
pip3 install --upgrade pip
pip3 install --user jupyter opencv-python torch
pip3 install --user numpy --upgrade
```

Next, we'll clone this repository
```
git clone https://github.com/mgb45/ENG5105
```

# Running the notebooks

Now we'll run jupyter notebook in a headless fashion
```
jupyter notebook --no-browser --port 8888 --ip 0.0.0.0
```

You can now access the notebook running on the raspberry pi using any other computer on the network, by simply typing
```
http://raspberry_pi_ip:8888/
```
into a browser address bar, where `raspberry_pi_ip` is the ip address of your raspberry pi. Eg. mine is `192.168.20.14`.

You can find out your raspberry pi ip address by typing `ifconfig` in a raspberry pi terminal, or going to your router settings pages and looking at the addresses of connected devices.

Use `ctrl-c` in the terminal to kill a running process (eg. if you want to close the notebook). Shutdown your pi cleanly with `sudo shutdown -h now`

