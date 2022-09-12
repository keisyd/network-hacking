# (Hashcat)[https://hashcat.net/hashcat/]

Hashcat is a password crakcer that cracks WPA and WPA-2 and now we have even a new mode 22000. So, it combines PMKIDs and EAPOL MESSAGE PAIRS in a single file which is a lot more efficient and also does not require a client connected to an access point and you don't have to knock it off either.

## Hashcat bruteforce attack

Requirements:

- A device connected to a newtork
- A wireless adapter that supports monitor mode
- (hcxdumptool)[https://github.com/ZerBea/hcxdumptool]

So, given the requirements, we are going to first see the wireless adapter with 

# Steps

After installing hcxumptool, we're going to stop all services that are accessing the wifi network

> sudo systemctl stop NetworkManager.service
> sudo systemctl stop wpa_supplicant.service

> sudo hcxdumptool -i wlan0 -o dumpfile.pcapng --active_beacon --enable_status=1



> hcxpcapngtool -o hash.hc22000 -E essidlist dumpfile.pcapng