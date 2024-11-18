Ubuntu 64bit with Docker for Raspberry Pi
==========================================

An out of the box `Raspberry Pi <http://www.raspberrypi.org/>`_ Ubuntu distro with a 64bit chroot with docker. 

Donate
------
UbuntuDockerPi is 100% free and open source and maintained by Guy Sheffer. If its helping your life, your organisation or makes you happy, please consider making a donation. It means I can code more and worry less about my balance. Any amount counts.
Also many thanks to people contributing code.

|paypal|

.. |paypal| image:: https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif
   :target: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=26VJ9MSBH3V3W&source=url

Where to get it?
----------------

You can use the `pi-imager <https://github.com/guysoft/pi-imager/releases>`_ commuity raspberrypi imager here, unofficial section.

Or download directly form the official mirror `here <http://unofficialpi.org/Distros/UbuntuDockerPi>`_

Nightly builds are available on pi-imager above or `here <http://unofficialpi.org/Distros/UbuntuDockerPi/nightly/>`_ (currently built on demand)

How to use it?
--------------

#. Unzip the image and install it to an SD card `like any other Raspberry Pi image <https://www.raspberrypi.org/documentation/installation/installing-images/README.md>`_
#. Configure your WiFi by editing ``ubuntudocker-wpa-supplicant.txt`` at the root of the flashed card when using it like a flash drive
#. Boot the Pi from the SD card
#. Hostname is ``ubuntudocker`` (not ``raspberrypi`` as usual)
#. Username is ``ubuntu`` initial password ``ubuntu``. You will be prompted to change it after first login.


Requirements
------------
* Raspberry Pi 3B+, 4B
* 2A power supply

Features
--------

* Ubuntu 64bit (aarch64) with docker
* Wifi file that lest you set up the Pi wifi out of the box, unlike official build that you need to plug and configfure and ethernet connection to download the wifi packages.
* Tools to configure the network via text files /boot

Developing
----------

Build UbuntuDockerPi
~~~~~~~~~~~~~~~~~~~~

UbuntuDockerPi can be built using docker running either on an intel or RaspberryPi (supported ones listed).
Build requires about 4.5 GB of free space available.
You can build it assuming you already have docker and docker-compose installed issuing the following commands::

    
    git clone https://github.com/guysoft/UbuntuDockerPi.git
    cd UbuntuDockerPi/src/image
    wget -c --trust-server-names 'https://cdimage.ubuntu.com/releases/24.04.1/release/ubuntu-24.04.1-preinstalled-desktop-arm64+raspi.img.xz'
    cd ..
    sudo docker-compose up -d
    sudo docker exec -it ubuntudockerpi-build build

Requirements
~~~~~~~~~~~~

#. You need to build this distro with a Raspberrypi with the 64bit kernel mode enabled, so it can run both armf and aarch64.
#. `CustomPiOS <https://github.com/guysoft/CustomPiOS>`_ using the Docker build method
#. root privileges for chroot
#. Bash

Building UbuntuDocker Variants
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Rasbian64 supports building variants, which are builds with changes from the main release build. An example and other variants are available in the folder ``src/variants/example``.

To build a variant use::

    sudo bash -x ./build_dist [Variant]
    
Usage
~~~~~

#. If needed, override existing config settings by creating a new file ``src/config.local``. You can override all settings found in ``src/config``. If you need to override the path to the Raspbian image to use for building Raspbian64, override the path to be used in ``ZIP_IMG``. By default, the most recent file matching ``ubuntu-*.xz`` found in ``src/image`` will be used.
#. Run ``src/build_dist`` as root.
#. The final image will be created in ``src/workspace``

Code contribution would be appreciated!
