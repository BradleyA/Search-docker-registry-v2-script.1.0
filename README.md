# Search-docker-registry-v2-script
[![GitHub Stable Release](https://img.shields.io/badge/Release-v2.3.2-blue.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/releases/tag/v2.3.2)
![GitHub Release Date](https://img.shields.io/github/release-date/BradleyA/Search-docker-registry-v2-script?color=blue)
[![GitHub Commits Since](https://img.shields.io/github/commits-since/BradleyA/Search-docker-registry-v2-script/v
?color=orange)](https://github.com/BradleyA/Search-docker-registry-v2-script/commits/)
[![GitHub Last Commits](https://img.shields.io/github/last-commit/BradleyA/Search-docker-registry-v2-script.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/commits/)

[![Open GitHub Issue](https://img.shields.io/badge/Open_an-Incident-brightgreen.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/issues/new/choose)
[![GitHub Open Issues](https://img.shields.io/github/issues/BradleyA/Search-docker-registry-v2-script?color=purple)](https://github.com/BradleyA/Search-docker-registry-v2-script/issues?q=is%3Aopen+is%3Aissue)
[![GitHub Closed Issues](https://img.shields.io/github/issues-closed/BradleyA/Search-docker-registry-v2-script?color=purple)](https://github.com/BradleyA/Search-docker-registry-v2-script/issues?q=is%3Aclosed+is%3Aissue)

[<img alt="GitHub Repo Clones" src="https://img.shields.io/static/v1?label=Repo_Clones&message=287&color=blueviolet">](https://github.com/BradleyA/Search-docker-registry-v2-script/blob/master/images/clone.table.md)
[<img alt="GitHub Repo Views" src="https://img.shields.io/static/v1?label=Repo_Views&message=4041&color=blueviolet">](https://github.com/BradleyA/Search-docker-registry-v2-script/blob/master/images/view.table.md)
[![GitHub Size](https://img.shields.io/github/repo-size/BradleyA/Search-docker-registry-v2-script.svg)](https://github.com/BradleyA/Search-docker-registry-v2-script/)
![Language Bash](https://img.shields.io/badge/%20Language-bash-blue.svg)
[![MIT License](http://img.shields.io/badge/License-MIT-blue.png)](LICENSE)

## Goal

List images on docker registry v2

#### If you like this repository, select in the upper-right corner, [![GitHub stars](https://img.shields.io/github/stars/BradleyA/Search-docker-registry-v2-script.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/BradleyA/Search-docker-registry-v2-script/stargazers/), thank you.

<details>
<summary>Table of content</summary>

## Table of content
- [Descriptions](#Descriptions)
- [Install](#Install)
- [Usage](#Usage)
- [Output](#Output)
- [TLS](#TLS)
----
- [Contribute](#Contribute)
- [Author](#Author)
- [Tested OS](#Tested-OS)
- [Design Principles](#Design-Principles)
- [License](#License)

</details>

----

## Descriptions

**view-private-registry** is a bash script for listing images in a private registry v2.  It does not require registry v2 to be running on the system, only the filesystem where the images are stored.  Docker search registry v2 functionality is currently not supported at the time of this writing. See discussion since Feb 2015: "propose registry search functionality #206" https://github.com/docker/distribution/issues/206

**view-private-registry-remote** is a bash script for listing images in a private registry v2 from a remote system that does not have the NFS filesystem mounted where the images are stored.  This script requires ssh to be installed and configured on the systems required to run this script.  This script calls the view-private-registry script that is on the host with the NFS filesystem mounted.

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

## Install

To Install, change into a directory that you want to download the scripts. Use git to pull or clone these scripts into the directory. If you do not have Git installed then enter; "sudo apt-get install git" if using Debian/Ubuntu. Other Linux distribution install methods can be found here: https://git-scm.com/download/linux. On the GitHub page of this script use the "HTTPS clone URL" with the 'git clone' command.

    git clone https://github.com/BradleyA/Search-docker-registry-v2-script
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

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

## Usage

    view-private-registry
or

    view-private-registry-remote

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

## Output

    $ view-private-registry
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

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

## TLS
I wrote a few scripts that may help you with the private registry and TLS.  The scripts are **create-registry-tls.sh**, **copy-registry-tls.sh**, and **check-registry-tls.sh** which can be found in [https://github.com/BradleyA/docker-security-infrastructure/blob/master/docker-TLS/README.md](https://github.com/BradleyA/docker-security-infrastructure/blob/master/docker-TLS/README.md).  These scripts support --help and --usage options to reduce the learning curve.

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

----

#### Contribute
Please do contribute! Issues and pull requests are welcome.  Thank you for your help improving software.

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### Author
[<img id="github" src="images/github.png" width="50" a="https://github.com/BradleyA/">](https://github.com/BradleyA/)    [<img src="images/linkedin.png" style="max-width:100%;" >](https://www.linkedin.com/in/bradleyhallen) [<img id="twitter" src="images/twitter.png" width="50" a="twitter.com/bradleyaustintx/">](https://twitter.com/bradleyaustintx/)       <a href="https://twitter.com/intent/follow?screen_name=bradleyaustintx"> <img src="https://img.shields.io/twitter/follow/bradleyaustintx.svg?label=Follow%20@bradleyaustintx" alt="Follow @bradleyaustintx" />    </a>          [![GitHub followers](https://img.shields.io/github/followers/BradleyA.svg?style=social&label=Follow&maxAge=2592000)](https://github.com/BradleyA?tab=followers)

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### Stars
[![Stargazers repo roster for @BradleyA/Search-docker-registry-v2-script.1.0](https://reporoster.com/stars/BradleyA/Search-docker-registry-v2-script.1.0)](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/stargazers)

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### Forks
[![Forkers repo roster for @BradleyA/Search-docker-registry-v2-script.1.0](https://reporoster.com/forks/BradleyA/Search-docker-registry-v2-script.1.0)](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/network/members)

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### Tested OS
 * CoreOS 723.3.0
 * Raspbian GNU/Linux 10 (buster)
 * Ubuntu 14.04.3 LTS (amd64,armv7l)
 * Ubuntu 16.04.7 LTS (amd64,armv7l)
 * Ubuntu 18.04.5 LTS (amd64,armv7l)

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### Design Principles
 * Have a simple setup process and a minimal learning curve
 * Be usable as non-root
 * Be easy to install and configure
 
 [Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)

#### License
MIT License

Copyright (c) 2021 [Bradley Allen](https://www.linkedin.com/in/bradleyhallen)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[Return to top](https://github.com/BradleyA/Search-docker-registry-v2-script.1.0/blob/master/README.md#search-docker-registry-v2-script)
