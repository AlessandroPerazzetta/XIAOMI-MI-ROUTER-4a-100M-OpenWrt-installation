# Steps:

- Install a dhcp and tftp server (set ethernet interface server for example at 192.168.10.1, and range pool at 192.168.10.10-20)
- Download Chinese stock version 2.18.28: (https://bigota.miwifi.com/xiaoqiang/rom/r4ac/miwifi_r4ac_all_c4b35_2.18.28.bin)
- Copy miwifi_r4ac_all_c4b35_2.18.28.bin to tftp server root path and name as test.bin (cp miwifi_r4ac_all_c4b35_2.18.28.bin /tftp/test.bin)
- Downgrade to 2.18.28, power up taking reset button until power led blink orange continuosly and wait until led come back blue
- Enter web interface at http://192.168.31.1 and complete setup, reboot
- Download Chinese stock version 2.18.51: (https://bigota.miwifi.com/xiaoqiang/rom/r4ac/miwifi_r4ac_firmware_e8a04_2.18.51.bin)
- Upgrade from 2.18.28 to 2.18.51, enter web interface at http://192.168.31.1 and go to section upgrade, upload miwifi_r4ac_firmware_e8a04_2.18.51.bin
- Clone OpenWRTInvasion repository: git clone https://github.com/acecilia/OpenWRTInvasion.git
- Enter the OpenWRTInvasion directory: cd OpenWRTInvasion
- Update system and install python3-pip: sudo apt update && sudo apt install python3-pip
- Install python requirements: pip3 install -r requirements.txt
- Enter web interface at http://192.168.31.1 and copy stok parameter value from url, something like stok=XXXX take XXXX part
- Root shell exploit with OpenWRTInvasion: python3 remote_command_execution_vulnerability.py (Run from the same pc)
- Enter ip address 192.168.31.1 and stok value
- Connect via telnet: telnet 192.168.31.1 with user root
- After entering BusyBox shell go to tmp: cd /tmp
- Download openwrt curl firmware: curl -k https://downloads.openwrt.org/releases/21.02.1/targets/ramips/mt76x8/openwrt-21.02.1-ramips-mt76x8-xiaomi_mi-router-4a-100m-squashfs-sysupgrade.bin --output firmware.bin
- Check sha with: ./busybox sha256sum firmware.bin, redownload if checksum is corrupt
- Install firmware: mtd -e OS1 -r write firmware.bin OS1
- Wait, ths can take at leat 10 min, until all led lights turno on blue

# Reference links:

https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_4a_100m
https://forum.openwrt.org/t/bricked-xiaomi-mi-router-4a-mir4a-100m-international-version/102391/8

https://www.youtube.com/watch?v=VxzEvdDWU_s
https://forum.openwrt.org/t/bricked-xiaomi-mi-router-4a-mir4a-100m-international-version/102391/8
