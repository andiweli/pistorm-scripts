# PiStorm Scipts
### Several PiStorm scripts, optimizations and enhancements
> The main purpose is/was for private use and backup and not to grab everything again from 10ish websites when rebuilding a PiStorm.

Sources used here are as follows:
* https://github.com/captain-amygdala/pistorm
* https://github.com/LemaruX/PiStorm-Firmware
* https://www.retro32.com/amiga-resources/240820213135-pistorm-installation-and-setup-guide-apps-pidisk-networking-and-rtg-a314
* https://github.com/captain-amygdala/pistorm/wiki/PiStorm-Software-Installation#Auto-starting-PiStorm-emulator
* https://www.hackster.io/kamaluddinkhan/changing-the-splash-screen-on-your-raspberry-pi-7aee31
* https://www.raspberry-pi-geek.de/ausgaben/rpg/2018/08/der-dateimanager-midnight-commander/
* https://tutorials-raspberrypi.de/raspberry-pi-samba-server-dateien-lokales-netzwerk-teilen/

## Let's start...

Assuming the Pi running BULLSEYE and is set-up and ready, WiFi is online, SSH is running and system is up to date with `sudo apt update && sudo apt upgrade`...

### Downloading and compiling PiStorm
* `sudo apt-get install git libasound2-dev libdrm-dev libegl1-mesa-dev libgles2-mesa-dev libgbm-dev`
* `git clone https://github.com/captain-amygdala/pistorm.git`
* `cd pistorm`
* `make PLATFORM=PI3_BULLSEYE`

Copy the amiga.cfg to default.cfg with `sudo cp amiga.cfg default.cfg` and configure it to your needs. It will load by default.

### Running PiStorm for test purposes
* `sudo ./emulator`

### Downloading the FPGA Update(s)
* `sudo apt-get install openocd`
* `git clone https://github.com/LemaruX/PiStorm-Firmware`
* `cd PiStorm-Firmware`

The available FPGA Firmwares are shown [here](https://github.com/LemaruX/PiStorm-Firmware#included-firmware).

### Autostarting PiStorm at boot-up
* `sudo nano /etc/systemd/system/pistorm.service`

```
[Unit]
Description=PiStorm emulator
After=network.target
StartLimitIntervalSec=0
[Service]
Type=simple
Restart=always
RestartSec=1
User=root
ExecStart=/home/pi/pistorm/emulator
WorkingDirectory=/home/pi/pistorm
[Install]
WantedBy=multi-user.target
```
* `sudo systemctl enable pistorm.service`
* `sudo systemctl daemon-reload`

