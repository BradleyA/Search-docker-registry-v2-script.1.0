# Search-docker-registry-v2-script
[<img alt="Clones" src="https://img.shields.io/static/v1?label=Clones&message=190&color=blue">](images/clone.table.md)
[<img alt="Views" src="https://img.shields.io/static/v1?label=Views&message=3071&color=blue">](images/view.table.md)

[![GitHub Stable Release](https://img.shields.io/badge/Release-v2.2-blue.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/releases/tag/v2.2)
![GitHub Release Date](https://img.shields.io/github/release-date/BradleyA/Search-docker-registry-v2-script?color=blue)
[![GitHub Commits Since](https://img.shields.io/github/commits-since/BradleyA/Search-docker-registry-v2-script/v2.2?color=orange)](https://github.com/BradleyA/Search-docker-registry-v2-script/commits/)
[![GitHub Last Commits](https://img.shields.io/github/last-commit/BradleyA/Search-docker-registry-v2-script.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/commits/)

[![GitHub Open Issues](https://img.shields.io/github/issues/BradleyA/Search-docker-registry-v2-script?color=purple)](https://github.com/BradleyA/Search-docker-registry-v2-script/issues?q=is%3Aopen+is%3Aissue)
[![GitHub Closed Issues](https://img.shields.io/github/issues-closed/BradleyA/Search-docker-registry-v2-script?color=purple)](https://github.com/BradleyA/Search-docker-registry-v2-script/issues?q=is%3Aclosed+is%3Aissue)
[<img alt="GitHub Clones" src="https://img.shields.io/static/v1?label=Clones&message=257&color=blueviolet">](https://github.com/BradleyA/Search-docker-registry-v2-script/blob/master/hooks/images/clone.table.md)
[<img alt="GitHub Views" src="https://img.shields.io/static/v1?label=Views&message=3488&color=blueviolet">](https://github.com/BradleyA/Search-docker-registry-v2-script/blob/master/hooks/images/view.table.md)
[![GitHub Size](https://img.shields.io/github/repo-size/BradleyA/Search-docker-registry-v2-script.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/)
![Written in Bash](https://img.shields.io/badge/written%20in-bash-blue.svg)
[![MIT License](http://img.shields.io/badge/License-MIT-blue.png)](LICENSE)


view-private-registry is a bash script for listing images in a private registry v2.  It does not require registry v2 to be running on the system, only the filesystem where the images are stored.  Docker search registry v2 functionality is currently not supported at the time of this writing. See discussion since Feb 2015: "propose registry search functionality #206" https://github.com/docker/distribution/issues/206

view-private-registry-remote is a bash script for listing images in a private registry v2 from a remote system that does not have the NFS filesystem mounted where the images are stored.  This script requires ssh to be installed and configured on the systems required to run this script.  This script calls the view-private-registry script that is on the host with the NFS filesystem mounted.
#### If you like this repository, select in the upper-right corner, STAR, thank you.

## Install
To install, change directory to the location you want to download the scripts.  Use git to pull or clone these scripts into the directory.  If you do not have git then enter; "sudo apt-get install git" if using Ubuntu.  On the github page of this script use the "HTTPS clone URL" with the 'git clone' command. 

    git clone https://github.com/BradleyA/Search-docker-registry-v2-script.git
    cd Search-docker-registry-v2-script

Edit view-private-registry script, change PERSISTENT_REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY to the path to your registry storage filesystem root directry.  It is the volume you used when starting the registry for /var/lib/registry.

     PERSISTENT_REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY="<your registry storage filesystem root directry>"

Move the script or create a symbolic link to a location in your working path; example /usr/local/bin. To find directories in your working path use; "echo $PATH".

    cp view-private-registry ..
    cd ..
    sudo ln -s $PWD/view-private-registry /usr/local/bin/view-private-registry
    
Edit view-private-registry-remote script, change REMOTE_REGISTRY_HOST to the remote host that has the registry v2 mounted, change REMOTE_ADMIN_ACCOUNT to the ssh admin account on the REMOTE_REGISTRY_HOST.  

     REMOTE_REGISTRY_HOST="<server IP address or FQDN>"
     REMOTE_ADMIN_ACCOUNT="<ssh admin account for the above host>"

Move the script or create a symbolic link to a location in your working path (see example above). 

## Usage

    view-private-registry
or

    view-private-registry-remote

## Output

    $ view-private-registry`
    busybox:latest
    gcr.io/google_containers/etcd:2.0.9
    gcr.io/google_containers/hyperkube:v0.21.2
    gcr.io/google_containers/pause:0.8.0
    google/cadvisor:latest
    jenkins:latest
    logstash:latest
    mongo:latest
    nginx:latest
    python:2.7
    redis:latest
    registry:2.1.1
    stackengine/controller:latest
    tomcat:7
    tomcat:latest
    ubuntu:14.04.2
    Number of images:   16
    Disk space used:    1.7G    /mnt/three/docker-registry/registry-data

#### Version of registry v2 using
 * registry github.com/docker/distribution v2.1.1
 
#### Registry with TLS
I wrote a few scripts that may help you with the private registry and TLS.  The scripts are [create-registry-tls.sh](https://github.com/BradleyA/docker-security-infrastructure/tree/master/docker-TLS#usage-9), [copy-registry-tls.sh](https://github.com/BradleyA/docker-security-infrastructure/tree/master/docker-TLS#usage-10), and [check-registry-tls.sh](https://github.com/BradleyA/docker-security-infrastructure/tree/master/docker-TLS#usage-11).   These scripts support --help and --usage options to reduce the learning curve.

#### Author
[<img id="github" src="images/github.png" width="50" a="https://github.com/BradleyA/">](https://github.com/BradleyA/)    [<img src="images/linkedin.png" style="max-width:100%;" >](https://www.linkedin.com/in/bradleyhallen) [<img id="twitter" src="images/twitter.png" width="50" a="twitter.com/bradleyaustintx/">](https://twitter.com/bradleyaustintx/)       <a href="https://twitter.com/intent/follow?screen_name=bradleyaustintx"> <img src="https://img.shields.io/twitter/follow/bradleyaustintx.svg?label=Follow%20@bradleyaustintx" alt="Follow @bradleyaustintx" />    </a>

#### System OS script tested
 * Ubuntu 14.04.3 LTS (amd64,armv7l)
 * CoreOS 723.3.0

#### Design Principles
 * Have a simple setup process and a minimal learning curve
 * Be usable as non-root
 * Be easy to install and configure

#### License
MIT License

Copyright (c) 2020 [Bradley Allen](https://www.linkedin.com/in/bradleyhallen)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
