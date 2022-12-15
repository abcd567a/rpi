## RPi Model 3 & 4 with 64-bit OS (arm64 / aarch64) <br> 
## Pre-built packages of piaware 8.2, dump1090-fa 8.2, piaware-web 8.2, dump978-fa 8.2, and beast-splitter 8.2, on following OS </br>
## (1) 64-bit Raspberry Pi OS Bullseye </br> 
## (2) 64-bit DietPi OS Bullseye </br>  
### [Links to download 64-bit OS](https://github.com/abcd567a/rpi/blob/master/README.md#links-to-download-64-bit-os-)
## How To Install Piaware arm64 Packages on Bullseye from this Personal Package Archive (PPA):


### STEP-1: Add this repository to list of apt sources by following 3 commands:
**First two commands are long. Please scroll right to see and copy them in FULL.** 
```
sudo wget -O /etc/apt/sources.list.d/abcd567a.list https://abcd567a.github.io/rpi/abcd567a.list
```
```
sudo wget -O /etc/apt/trusted.gpg.d/abcd567a-key.gpg https://abcd567a.github.io/rpi/KEY2.gpg
```
```
sudo apt update  
```

</br>

### STEP-2: Install packages
```
sudo apt install piaware  
```
```
sudo apt install dump1090-fa  
```
```
sudo apt install piaware-web  
```
```
sudo piaware-config feeder-id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 
```
```
sudo reboot 
```

&nbsp;

### STEP-3: (for USA only) Additional steps to install & configure dump978-fa

```
sudo apt install dump978-fa  
```
```
sudo piaware-config uat-receiver-type sdr  
```

**Configure dump1090-fa and dump978-fa to use their respective dongles.**
If you want to receive both ES1090 and UAT978, then two dongles are required, one for 1090 MHz and other for 978 MHz. In this case you will have to serialize dongles so that correct dongle+antenna sets are used by dump1090-fa and dump978-fa.
Serialize dongles with following serial numbers </br>

**For 1090 Mhz dongle: use 8-digit serial # 00001090** </br>
**For 978 Mhz dongle : use 8-digit serial # 00000978** </br>

After Serializing dongles with serial numbers as above, issue following commands to configure dump1090-fa and dump978-fa to use their respective dongles:

```
sudo sed -i 's/^RECEIVER_SERIAL=.*/RECEIVER_SERIAL=00001090/' /etc/default/dump1090-fa  
```
```
sudo sed -i 's/driver=rtlsdr[^ ]* /driver=rtlsdr,serial=00000978 /' /etc/default/dump978-fa  
```  
```
sudo reboot 
```

## How to Serialize Dongles:
(1) Issue following command to install serialization software: </br>
`sudo apt install rtl-sdr ` </br>

(2) Unplug ALL DVB-T dongles from RPi

(3) Plugin only that DVB-T dongle which you want to use for dump1090-fa. All other dongles should be unplugged.

(4) Issue following command. </br>
`rtl_eeprom -s 00001090 ` </br>
Say yes when asked for confirmation to change serial number.


(5) Unplug 1090 dongle

(6) Plugin only that DVB-T dongle which you want to use for dump978-fa. All other dongles should be unplugged.

(7) Issue following command. </br>
`rtl_eeprom -s 00000978 ` </br>
Say yes when asked for confirmation to change serial number.


(8) Unplug 978 dongle

IMPORTANT: After completing above commands, unplug and then replug both dongles.

&nbsp;

### OPTIONAL ITEM - beast-splitter
```
sudo apt install beast-splitter
```

**NOTE:** </br>
By default, the package beast-splitter wont start at boot. To enable it to automatically start at boot, do following:</br>
```
sudo nano /etc/default/beast-splitter  
```

In above file, change </br>
ENABLED="**no**" </br>
to </br>
ENABLED="**yes**" </br>

Save file (Ctrl+O) Closed (Ctrl+X) </br>

```
sudo reboot  
```

&nbsp;
## How to remove this repository from your RPi:

Deleting this repository from your Pi’s apt sources list is simple. Just issue following 2 command and it is done:

```
sudo rm /etc/apt/sources.list.d/abcd567a.list 
```
```
sudo apt update 
```


</br>

## Links to Download 64-bit OS </br>
### The 64-bit Raspberry Pi OS image can be downloaded from following pages: 
**Lite:** **[https://downloads.raspberrypi.org/raspios_lite_arm64/images/](https://downloads.raspberrypi.org/raspios_lite_arm64/images/)** </br>
**Full:** **[https://downloads.raspberrypi.org/raspios_arm64/images/](https://downloads.raspberrypi.org/raspios_arm64/images/)** </br>

### The 64-bit DietPi OS image can be downloaded from following page:
**[https://dietpi.com/#downloadinfo](https://dietpi.com/#downloadinfo)** </br>


&nbsp;
