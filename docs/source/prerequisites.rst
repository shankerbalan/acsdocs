Prerequisites
=============

In this section we'll look at installing the dependencies you'll need
for Apache CloudStack development.

On Ubuntu 12.04
---------------

First update and upgrade your system:

::

    apt-get update 
    apt-get upgrade

NTP might already be installed, check it with ``service ntp status``. If
it's not then install NTP to synchronize the clocks:

::

    apt-get install openntpd

Install ``openjdk``. As we're using Linux, OpenJDK is our first choice.

::

    apt-get install openjdk-6-jdk

Install ``tomcat6``, note that the new version of tomcat on
`Ubuntu <http://packages.ubuntu.com/precise/all/tomcat6>`__ is the
6.0.35 version.

::

    apt-get install tomcat6

Next, we'll install MySQL if it's not already present on the system.

::

    apt-get install mysql-server

Remember to set the correct ``mysql`` password in the CloudStack
properties file. Mysql should be running but you can check it's status
with:

::

    service mysql status

Developers wanting to build CloudStack from source will want to install
the following additional packages. If you dont' want to build from
source just jump to the next section.

Install ``git`` to later clone the CloudStack source code:

::

    apt-get install git

Install ``Maven`` to later build CloudStack

::

    apt-get install maven

This should have installed Maven 3.0, check the version number with
``mvn --version``

A little bit of Python can be used (e.g simulator), install the Python
package management tools:

::

    apt-get install python-pip python-setuptools

Finally install ``mkisofs`` with:

::

    apt-get install genisoimage

On centOS 6.4
-------------

First update and upgrade your system:

::

    yum -y update
    yum -y upgrade

If not already installed, install NTP for clock synchornization

::

    yum -y install ntp

Install ``openjdk``. As we're using Linux, OpenJDK is our first choice.

::

    yum -y install java-1.6.0-openjdk

Install ``tomcat6``, note that the version of tomcat6 in the default
CentOS 6.4 repo is 6.0.24, so we will grab the 6.0.35 version. The
6.0.24 version will be installed anyway as a dependency to cloudstack.

::

    wget https://archive.apache.org/dist/tomcat/tomcat-6/v6.0.35/bin/apache-tomcat-6.0.35.tar.gz
    tar xzvf apache-tomcat-6.0.35.tar.gz -C /usr/local

Setup tomcat6 system wide by creating a file
``/etc/profile.d/tomcat.sh`` with the following content:

::

    export CATALINA_BASE=/usr/local/apache-tomcat-6.0.35
    export CATALINA_HOME=/usr/local/apache-tomcat-6.0.35

Next, we'll install MySQL if it's not already present on the system.

::

    yum -y install mysql mysql-server

Remember to set the correct ``mysql`` password in the CloudStack
properties file. Mysql should be running but you can check it's status
with:

::

    service mysqld status

Install ``git`` to later clone the CloudStack source code:

::

    yum -y install git

Install ``Maven`` to later build CloudStack. Grab the 3.0.5 release from
the Maven `website <http://maven.apache.org/download.cgi>`__

::

    wget http://mirror.cc.columbia.edu/pub/software/apache/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz
    tar xzf apache-maven-3.0.5-bin.tar.gz -C /usr/local
    cd /usr/local
    ln -s apache-maven-3.0.5 maven

Setup Maven system wide by creating a ``/etc/profile.d/maven.sh`` file
with the following content:

::

    export M2_HOME=/usr/local/maven
    export PATH=${M2_HOME}/bin:${PATH}

Log out and log in again and you will have maven in your PATH:

::

    mvn --version

This should have installed Maven 3.0, check the version number with
``mvn --version``

A little bit of Python can be used (e.g simulator), install the Python
package management tools:

::

    yum -y install python-setuptools

To install python-pip you might want to setup the Extra Packages for
Enterprise Linux (EPEL) repo

::

    cd /tmp
    wget http://mirror-fpt-telecom.fpt.net/fedora/epel/6/i386/epel-release-6-8.noarch.rpm
    rpm -ivh epel-release-6-8.noarch.rpm

Then update you repository cache ``yum update`` and install pip
``yum -y install python-pip``

Finally install ``mkisofs`` with:

::

    yum -y install genisoimage

