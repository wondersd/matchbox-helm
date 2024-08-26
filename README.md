# Testing DHCP Proxy #

https://matchbox.psdn.io/network-setup/

From an existing coreos install on the target network

```
sudo podman run --network=host --privileged jonlabelle/network-tools nmap --script broadcast-dhcp-discover
```

The above does not add enough informaiton on the request to trigger adding pxe boot options

```
Starting Nmap 7.95 ( https://nmap.org ) at 2024-08-24 17:46 UTC
Pre-scan script results:
| broadcast-dhcp-discover: 
|   Response 1 of 1: 
|     Interface: end0
|     IP Offered: 192.168.1.249
|     DHCP Message Type: DHCPOFFER
|     Server Identifier: 192.168.1.1
|     IP Address Lease Time: 12h00m00s
|     Renewal Time Value: 6h00m00s
|     Rebinding Time Value: 10h30m00s
|     Subnet Mask: 255.255.255.0
|     Broadcast Address: 192.168.1.255
|     Router: 192.168.1.1
|     Domain Name Server: 192.168.1.1
|_    Domain Name: lan
Nmap done: 0 IP addresses (0 hosts up) scanned in 10.61 seconds
WARNING: No targets were specified, so 0 hosts scanned.
```

output from proxydhcp

```
dnsmasq-dhcp: 1746075579 available DHCP subnet: 192.168.1.1/255.255.255.0
```

The output from a working bare metal machine pxe booting

```
dnsmasq-dhcp: 335816787 available DHCP subnet: 192.168.1.1/255.255.255.0
dnsmasq-dhcp: 335816787 vendor class: PXEClient:Arch:00007:UNDI:003016
dnsmasq-dhcp: 335816787 PXE(end0) xx:xx:xx:xx:xx:xx proxy
dnsmasq-dhcp: 335816787 tags: end0
dnsmasq-dhcp: 335816787 next server: 192.168.1.38
dnsmasq-dhcp: 335816787 broadcast response
dnsmasq-dhcp: 335816787 sent size:  1 option: 53 message-type  2
dnsmasq-dhcp: 335816787 sent size:  4 option: 54 server-identifier  192.168.1.38
dnsmasq-dhcp: 335816787 sent size:  9 option: 60 vendor-class  yy:yy:yy:yy:yy:yy:yy:yy:yy
dnsmasq-dhcp: 335816787 sent size: 17 option: 97 client-machine-id  00:xx:xx:xx:xx:xx:xx:00:00:00:00:00:00:00...
dnsmasq-dhcp: 335816787 available DHCP subnet: 192.168.1.1/255.255.255.0
dnsmasq-dhcp: 335816787 vendor class: PXEClient:Arch:00007:UNDI:003016
dnsmasq-dhcp: 335816787 PXE(end0) xx:xx:xx:xx:xx:xx proxy
dnsmasq-dhcp: 335816787 tags: end0
dnsmasq-dhcp: 335816787 next server: 192.168.1.38
dnsmasq-dhcp: 335816787 broadcast response
dnsmasq-dhcp: 335816787 sent size:  1 option: 53 message-type  2
dnsmasq-dhcp: 335816787 sent size:  4 option: 54 server-identifier  192.168.1.38
dnsmasq-dhcp: 335816787 sent size:  9 option: 60 vendor-class  yy:yy:yy:yy:yy:yy:yy:yy:yy
dnsmasq-dhcp: 335816787 sent size: 17 option: 97 client-machine-id  00:xx:xx:xx:xx:xx:xx:00:00:00:00:00:00:00...
dnsmasq-dhcp: 335816787 available DHCP subnet: 192.168.1.1/255.255.255.0
dnsmasq-dhcp: 335816787 vendor class: PXEClient:Arch:00007:UNDI:003016
```