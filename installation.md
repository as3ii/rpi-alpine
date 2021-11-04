# Installation Procedure

## RPi preparation

_Note: if you reboot the RPi during this phase you have to redo steps 5, 6 and
the second point of step 7_

1. Partition the device:
    - MBR Partition Table
    - 150MB FAT32 partition
    - Remaining ext4
2. Download alpine from the [official website](https://alpinelinux.org/downloads/)
In the "Raspberry Pi" section select one of the possible archive:
    - armhf: compatible with every RPis
    - armv7: not compatible with RPi 1, 0 or 0W
    - aarch64: not compatible with RPi 2, 1, 0 or 0W
3. Copy the content of the `.tar.gz` inside the first partition:
    - mount the first partition
    - `cd` into it
    - `tar xzf path/to/file.tar.gz`
4. Run the following commands to set gpu_mem=32 and enable HDMI hotplug:
    - `printf "\ngpu_mem=32\nhdmi_force_hotplug=1\n" >> config.txt`
5. Unmount the SD card, plug it in the RPi with keyboard and monitor
6. Login using username "root" and empty password
7. Run the following commands in the RPi terminal:
    - (optional) `setup-keymap`: setup keyboard layout
    - `passwd`: set a temporary root password
    - `setup-interfaces`: setup the eth0 network interface
    - `/etc/init.d/networking start`: start the network stack
    - `setup-sshd`: install ssh server and enable the service
    - `sed -i 's/^#PermitRootLogin .*$/PermitRootLogin yes/' /etc/ssh/sshd_config`
    - `/etc/init.d/sshd restart`: restart sshd
8. Came back to your PC:
    - generate an ssh key if you don't have one or if you want to have a new key:
        - run `ssh-keygen` to generate a key using the default options
    - run `ssh-copy-id root@IP` command to copy the key to the RPi
        - substitute `IP` with the IP of the RPi (you can discover it
        running `ip address show` or the abbreviated `ip a` inside the
        RPi terminal)
        - you can specify a particular ssh key using `-i path/to/the/key`
9. From now on you can unplug monitor and keyboard and use only ssh, unless
you accidentally reboot the RPi before completing the installation


## PC preparation

1. Install Ansible, some possible ways are:
    - using the package manager of your linux distribution
    - using run `pip` to install ansible system-wide:
        - `sudo pip install ansible`
    - using `pip` to install ansible for the current user:
        - (optional) create a python's venv and activate it
        - run `pip install ansible`

    For more info see [the official documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
2. Clone this repository if you hadn't already done
    - `git clone https://github.com/as3ii/rpi-alpine.git`
3. Edit the `inventory` file:
    - put in the right section the IP's of your RPi's
    - check if the ssh user and key are correct in the `rpis:vars` section

## Installation
_To Do_


