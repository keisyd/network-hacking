# (Hashcat)[https://hashcat.net/hashcat/]

Hashcat is a password crakcer that cracks WPA and WPA-2 and now we have even a new mode 22000. So, it combines PMKIDs and EAPOL MESSAGE PAIRS in a single file which is a lot more efficient and also does not require a client connected to an access point and you don't have to knock it off either.

## Hashcat bruteforce attack

Requirements:

- A device connected to a newtork
- A wireless adapter that supports monitor mode
- (hcxdumptool)[https://github.com/ZerBea/hcxdumptool]

So, given the requirements, we are going to first see the wireless adapter with 

# Steps

Shut down all the services using the network adapter

> sudo systemctl stop NetworkManager.service
> sudo systemctl stop wpa_supplicant.service

And then we need to let *hcxdumptool* scan all networks for information before we start hacking.

> sudo hcxdumptool -i