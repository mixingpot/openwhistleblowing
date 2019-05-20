

3309/5000
# Openwhistleblowing

## Introduction
This repository contains the source code and the binary ready for
the installation of Openwhistleblowing (release 1.0.1), the software supplied for
reused by the ANAC (National Anti-Corruption Authority).

## Installation
In order to allow the widest possible personalization to the Administrations
users of the software, the same is supplied complete with source. IS
You can install it in one of the following ways:

- installation using rpm (RedHat Package Manager)
- installation using Docker
- installation from source (using maven)

The prerequisites for installation are:
- RedHat Enterprise Linux or Centos 7 operating system. *
- 100 GB of attachment storage disk
- 4 GB RAM (suggested 8)

At the end of the installation the users default password is password1

### RPM
Installation using RPM is performed or using the script in src / scripts / install.sh,
or by manually launching the following instructions:

`` `Bash
cd openwhistleblowing
yum -y install epel-release
yum -y install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-6-x86_64/pgdg-centos96-9.6-3.noarch.rpm
yum -y install postgresql96-devel
yum -y install ../../binary/owb-1.0.1-1.x86_64.rpm &> / dev / null
`` `
The configuration of the tool can initially be done using the script
present in src / scripts / setup.sh. For more configuration options, refer to the documentation
project technique.

### Docker
Docker installation assumes that Docker is up and running (
refer to the documentation for [RedHat] (https://docs.docker.com/install/linux/docker-ee/rhel/) or
[Centos] (https://docs.docker.com/install/linux/docker-ce/centos/)).
The first step is to create the container image
`` `Bash
cd openwhistleblowing
docker build -t owb: anac.
`` `
then you can start the container with the following command (for customization
of the container start command, refer to the specific docker documentation)
`` `Bash
docker run -d --restart = unless-stopped --name = owb -p 80:80 -v / data: / var / owb / files owb: anac
`` `
the container accepts two environment variables:

| name | value |
| --------------------------- |: ---------: |
| EXTERNAL_HOSTNAME | string |
| DISABLE_MAIL_NOTIFICATION | 0 |

the first one, allows to insert the hostname with which the service is reached (e.g. myhost.mydomain.local),
the second one allows you to enable the email sending service (disabled by default).

For a subsequent configuration it is possible to enter the container in execution:
`` `Bash
docker exec -it owb / bin / bash
`` `
make the changes and restart the tool with:
`` `Bash
/etc/init.d/owb restart
`` `

### Source
The installation from source allows the most extensive customization of the application. It is
provided the pom.xml for the creation of the rpm which will subsequently be installed as
from previous instructions.
For packaging, it is necessary to install [maven] (https://maven.apache.org/) e
launch the following command:
`` `Bash
cd openwhistleblowing
mvn package
`` `
at the end of the execution the new rpm generated will be found in the path:
* Target / rpm / owb / RPMS / x86_64 / *
Send feedback
History
Saved
Community
