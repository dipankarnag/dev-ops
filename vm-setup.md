## Step 1:
Install Oracle Virtual Box.

## Step 2:
Go to VirtualBox installed location and find VBoxManage.exe. Then add the path to PATH variable so that VBoxManage can be used globally.

## Step 3:
Download Ubuntu Server 18.04LTS mini.iso which will eventually use internet to download all required packages.

## Step 4:
Create VM with Storage of 40GB, 2GM of RAM and 4 Processors. Go to Devices in its settings and show the mini.iso for installation.
Start the VM and install Ubuntu. Most of the steps are easy going. But while creating partitions choose mannual option and allocate as follows:
* Minimum of 3GM swap area
* 20GB for root partition; boot option will be on for this
* Put the rest of volume for home partition

Also while choosing the install package option choose Standard or Basic Ubuntu Server edition so that it will not come with GUI support which makes things unnecessarily slower.
And don't forget to choose OPENSSH option, however it can be installed later.


## Step 5:
Go to network option in VM's setting and in advanced option click "Port Forwarding"
Enter a new enrty with ports 2202 (Host) and 22 (Guest) leaving other fields empty.
This will forward all incoming requests on port 2202 from 127.0.0.1 to Guest OS on port 22 (defult ssh port).


## Step 6:
Assuming the VM is down, go to terminal/console/git-bash and run the following command:
```
VBoxManage list vms [This will list all the VMs look for your created ubuntu server VM]
VBoxManage startvm "[VM Name]" --type headless [This will start the VM without bothering about Oracle VM GUI and make things faster]
Open Putty and connect to 127.0.0.1 on port 2202 and start using the ubuntu server.
```