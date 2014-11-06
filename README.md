Tontec-RPi-Screen
=================

How to set up a Tontec screen on a Raspberry Pi. I used [this screen on Amazon](http://www.amazon.com/gp/product/B00LN9MYCO).

All of these commands assume sudo/root.

# Setup

## System

### Install Packages

    aptitude update
    aptitude install build-essential zip

### Set Screen Resolution

    nano /boot/config.txt

Change:

    #framebuffer_width=1280
    #framebuffer_height=720

To:

    framebuffer_width=480
    framebuffer_height=320

## Screen

### Get Driver

    cd /home/pi
    wget https://s3.amazonaws.com/ttbox/35screen.zip
    unzip 35screen.zip
    cd 35screen.zip
    unzip mzl350i-pi-ext.zip
    mv mzl350i-pi-ext /home/pi/mzl350i-pi-ext

### Edit Driver Config

    cd /home/pi/mzl350i-pi-ext/src
    nano mzl350i.c

Change:

    loadFrameBuffer_diff_960640();
  
To:

    loadFrameBuffer_diff_480320();

Save the file, and...

    make

### Set to Run on Startup

    crontab -e
    @reboot /home/pi/mzl350i-pi-ext/lcd

[Source](http://www.raspberrypi.org/forums/viewtopic.php?f=91&t=81022&p=600832&hilit=mzl350i#p600832)


## Terminal

### Set Font Size (Optional)

    nano /etc/default/console-setup

Set

    FONTSIZE="20x10"
    
[Source](http://unix.stackexchange.com/questions/49779/can-i-change-the-font-of-terminal)

### Disable Raspberry Logo (Optional)

    nano /boot/cmdline.txt

Set

    logo.nologo

[Source](http://www.raspberrypi.org/forums/viewtopic.php?f=31&t=11642)
