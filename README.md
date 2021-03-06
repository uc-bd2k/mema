### mema: Docker container for using MEMA R package in RStudio

This mema docker image was built based on the validated MEMA R package v1.0.1 (released on 2017-05-16) to run all the R code in the vignettes created by MEP-LINCS project on 2017-05-17 at [`https://github.com/MEP-LINCS/MEMA/tree/master/vignettes`](https://github.com/MEP-LINCS/MEMA/tree/master/vignettes) inside a virtual RStudio.

The container has been tested on Linux (Ubuntu 14.04 and 16.04), macOS (10.11.6), and Windows (Windows 7 Enterprise). 

---
#### Installation of Docker

Ubuntu: follow [`the instructions`](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/) to get Docker CE for Ubuntu.


Mac: follow [`the instructions`](https://store.docker.com/editions/community/docker-ce-desktop-mac) to install [`the Stable verion of Docker CE`](https://download.docker.com/mac/stable/Docker.dmg) on Mac.

Windows: follow [`the instructions`](https://docs.docker.com/toolbox/toolbox_install_windows/) to install [`Docker Tookbox`](https://download.docker.com/win/stable/DockerToolbox.exe) on Windows.

---
To obtain the docker image and run the container,
```
[sudo] docker pull ucbd2k/mema:stable
```
Please note that on Mac and Linux systems using docker without "sudo" requires post-installation setup. We noticed that in some cases misconfiguration may lead to a situation in which the container runs seemingly fine, but the code in vignettes fails to execute properly. Using "sudo" in these situations solved the problem.

We recommend a minimum of 8 GB memory to run the  MEMA vignettes. On Mac and Windows the memory needs to be manually allocated.

On Mac, click Docker whale icon in Launchpad or Applications folder to start Docker, then click Docker icon in top status bar and choose Preferences -> Advanced to increase Memory to 8.0 GB. 

On Windows, double-click Open Oracle VM VirtualBox icon on desktop, choose Settings -> System -> Motherboard to increase Base Memory to 8192 MB. 

To run the container execute the following command:

```
[sudo] docker run -d -p <an available port>:8787 ucbd2k/mema:stable
```
Typically one can use port 8787 if not already used by another application. In that case the commad is

```
[sudo] docker run -d -p 8787:8787 ucbd2k/mema:stable
```

To start an RStudio session, open a browser and type in the address bar ``<Host URL>:<available port as specified>``. Enter `rstudio` for both username and password. For example `http://localhost:8787` on Mac or Linux systems when 8787 port is used.

Host URL on Ubuntu and Mac is `localhost`, if accessed locally. On Windows, the IP is shown when Docker is launched by double-clicking the Docker Quickstart Terminal icon on desktop, or it can be obtained from the output of `docker-machine ls` in the interactive shell window.

To execute MEMA package vignettes, you need to have a Synapse account (register at [`https://www.synapse.org/`](https://www.synapse.org/#!RegisterAccount:0) and then create `.synapseConfig` file with your login credentials. For example, if the Synapse user account is `john.doe@fake.com` and password is `pass123`, the following R command executed in the RStudio session will create the appropriate config file:
```
cat(file="~/.synapseConfig", "[authentication]", "\n", 
    "username:john.doe@fake.com", "\n", 
    "password:pass123", "\n")

```
Now you can run the current MEMA vignettes packaged within the container. To do this, open the Rmd files in the vignettes_MEP-LINCS_2017-05-17 directory in the RStudio file browser.  The code can be exectued whole via RStudio knit toolbar ("Knit to HTML"), or by executing individual chunks of code interactively. 

To download and run the most recent version of vignettes from github, execute following commands in RStudio. 
```
download.file("https://raw.githubusercontent.com/MEP-LINCS/MEMA/master/vignettes/Preprocess-Levels1and2.Rmd",
    destfile="~/Preprocess-Levels1and2.Rmd")
download.file("https://raw.githubusercontent.com/MEP-LINCS/MEMA/master/vignettes/Preprocess-Levels3and4.Rmd",
destfile="~/Preprocess-Levels3and4.Rmd")
```
Vignettes can now be opened by clicking on the file link in the RStudio file browser.  






