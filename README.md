# CCNA-MegaLab

This comprehensive lab covers all configuration topics on the CCNA exam.

<img width="1073" height="638" alt="diagram" src="https://github.com/user-attachments/assets/085fb9a4-eb59-4111-93f5-6ba91c5db1e7" />

## Part 1 - Initial Setup
1. Configure the appropriate hostname on each router/switch.
2. Configure the enable secret jeremysitlab on each router/switch. Use type 9 hashing if available; otherwise, use type 5.
3. Configure the user account cisco with secret ccna on each router/switch. Use type 9 hashing if available; otherwise, use type 5.
4. Configure the console line to require login with a local user account. Set a 30-minute inactivity timeout. Enable synchronous logging.

## Part 2 – VLANs, Layer-2 EtherChannel
1. **Office A:**
   - Configure a Layer-2 EtherChannel named **PortChannel1** between **DSW-A1** and **DSW-A2** using a Cisco-proprietary protocol.  
   - Both switches should actively try to form an EtherChannel.

2. **Office B:**
   - Configure a Layer-2 EtherChannel named **PortChannel1** between **DSW-B1** and **DSW-B2** using an open standard protocol.  
   - Both switches should actively try to form an EtherChannel.

3. **Trunk Links:**
   - Configure all links between Access and Distribution switches, including the EtherChannels, as trunk links.
     - a. Explicitly disable DTP on all ports.  
     - b. Set each trunk’s native VLAN to **VLAN 1000 (unused)**.  
     - c. In Office A, allow VLANs **10, 20, 40, and 99** on all trunks.  
     - d. In Office B, allow VLANs **10, 20, 30, and 99** on all trunks.  

4. **VTP Configuration:**
   - Configure one of each office’s Distribution switches as a **VTPv2 server**. Use domain name **JeremysITLab**.  
     - a. Verify that other switches join the domain.  
     - b. Configure all Access switches as **VTP clients**.  

5. **Office A VLANs:**
   - Create and name the following VLANs on one of the Distribution switches. Ensure that VTP propagates the changes:  
     - VLAN 10: **PCs**  
     - VLAN 20: **Phones**  
     - VLAN 40: **Wi-Fi**  
     - VLAN 99: **Management**  

6. **Office B VLANs:**
   - Create and name the following VLANs on one of the Distribution switches. Ensure that VTP propagates the changes:  
     - VLAN 10: **PCs**  
     - VLAN 20: **Phones**  
     - VLAN 30: **Servers**  
     - VLAN 99: **Management**  

7. **Access Ports:**
   - Configure each Access switch’s access port.  
     - a. LWAPs will not use FlexConnect.  
     - b. PCs in **VLAN 10**, Phones in **VLAN 20**.  
     - c. **SRV1** in **VLAN 30**.  
     - d. Manually configure access mode and explicitly disable DTP.  

8. **ASW-A1 to WLC1 Connection:**
   - Configure ASW-A1’s connection to **WLC1**:  
     - a. It must support the **Wi-Fi** and **Management VLANs**.  
     - b. The **Management VLAN** should be **untagged**.  
     - c. Disable DTP.  

9. **Unused Ports:**
   - Administratively disable all unused ports on Access and Distribution switches.

# Part 3 – IP Addresses, Layer-3 EtherChannel, HSRP

1. **R1 Interfaces:**
   - G0/0/0: **DHCP client**
   - G0/1/0: **DHCP client**
   - G0/0: **10.0.0.33/30**
   - G0/1: **10.0.0.37/30**
   - Loopback0: **10.0.0.76/32**

2. **Enable IPv4 routing** on all Core and Distribution switches.

3. **Layer-3 EtherChannel (CSW1 ↔ CSW2):**
   - Use a Cisco-proprietary protocol.  
   - Both switches should actively try to form an EtherChannel.  
   - IPs:  
     - CSW1 PortChannel1: **10.0.0.41/30**  
     - CSW2 PortChannel1: **10.0.0.42/30**

4. **CSW1 IP Configuration (disable unused interfaces):**
   - G1/0/1: **10.0.0.34/30**
   - G1/1/1: **10.0.0.45/30**
   - G1/1/2: **10.0.0.49/30**
   - G1/1/3: **10.0.0.53/30**
   - G1/1/4: **10.0.0.57/30**
   - Loopback0: **10.0.0.77/32**

5. **CSW2 IP Configuration (disable unused interfaces):**
   - G1/0/1: **10.0.0.38/30**
   - G1/1/1: **10.0.0.61/30**
   - G1/1/2: **10.0.0.65/30**
   - G1/1/3: **10.0.0.69/30**
   - G1/1/4: **10.0.0.73/30**
   - Loopback0: **10.0.0.78/32**

6. **DSW-A1:**
   - G1/1/1: **10.0.0.46/30**
   - G1/1/2: **10.0.0.62/30**
   - Loopback0: **10.0.0.79/32**

7. **DSW-A2:**
   - G1/1/1: **10.0.0.50/30**
   - G1/1/2: **10.0.0.66/30**
   - Loopback0: **10.0.0.80/32**

8. **DSW-B1:**
   - G1/1/1: **10.0.0.54/30**
   - G1/1/2: **10.0.0.70/30**
   - Loopback0: **10.0.0.81/32**

9. **DSW-B2:**
   - G1/1/1: **10.0.0.58/30**
   - G1/1/2: **10.0.0.74/30**
   - Loopback0: **10.0.0.82/32**

10. **SRV1 Manual IP:**
    - Default Gateway: **10.5.0.1**  
    - IPv4 Address: **10.5.0.4**  
    - Subnet Mask: **255.255.255.0**

11. **Access Switch Management IPs (VLAN 99):**
    - ASW-A1: **10.0.0.4/28**
    - ASW-A2: **10.0.0.5/28**
    - ASW-A3: **10.0.0.6/28**
    - ASW-B1: **10.0.0.20/28**
    - ASW-B2: **10.0.0.21/28**
    - ASW-B3: **10.0.0.22/28**  
    > Use the first usable address in each subnet as the **default gateway**.

---

### HSRP Configuration

#### Office A
12. **HSRPv2 Group 1 – Management (VLAN 99):**
   - Subnet: **10.0.0.0/28**  
   - VIP: **10.0.0.1**  
   - DSW-A1: **10.0.0.2** (Active, Priority +5, Preempt)  
   - DSW-A2: **10.0.0.3**

13. **HSRPv2 Group 2 – PCs (VLAN 10):**
   - Subnet: **10.1.0.0/24**  
   - VIP: **10.1.0.1**  
   - DSW-A1: **10.1.0.2** (Active, Priority +5, Preempt)  
   - DSW-A2: **10.1.0.3**

14. **HSRPv2 Group 3 – Phones (VLAN 20):**
   - Subnet: **10.2.0.0/24**  
   - VIP: **10.2.0.1**  
   - DSW-A1: **10.2.0.2**  
   - DSW-A2: **10.2.0.3** (Active, Priority +5, Preempt)  

15. **HSRPv2 Group 4 – Wi-Fi (VLAN 40):**
   - Subnet: **10.6.0.0/24**  
   - VIP: **10.6.0.1**  
   - DSW-A1: **10.6.0.2**  
   - DSW-A2: **10.6.0.3** (Active, Priority +5, Preempt)  

### Office B
16. **HSRPv2 Group 1 – Management (VLAN 99):**
   - Subnet: **10.0.0.16/28**  
   - VIP: **10.0.0.17**  
   - DSW-B1: **10.0.0.18** (Active, Priority +5, Preempt)  
   - DSW-B2: **10.0.0.19**

17. **HSRPv2 Group 2 – PCs (VLAN 10):**
   - Subnet: **10.3.0.0/24**  
   - VIP: **10.3.0.1**  
   - DSW-B1: **10.3.0.2** (Active, Priority +5, Preempt)  
   - DSW-B2: **10.3.0.3**

18. **HSRPv2 Group 3 – Phones (VLAN 20):**
   - Subnet: **10.4.0.0/24**  
   - VIP: **10.4.0.1**  
   - DSW-B1: **10.4.0.2**  
   - DSW-B2: **10.4.0.3** (Active, Priority +5, Preempt)  

19. **HSRPv2 Group 4 – Servers (VLAN 30):**
   - Subnet: **10.5.0.0/24**  
   - VIP: **10.5.0.1**  
   - DSW-B1: **10.5.0.2**  
   - DSW-B2: **10.5.0.3** (Active, Priority +5, Preempt)

## Part 4 – Rapid Spanning Tree Protocol
1. Configure Rapid PVST+ on all Access and Distribution switches.
    - Ensure that the Root Bridge for each VLAN aligns with the HSRP Active router by configuring the lowest possible STP priority.
    - Configure the HSRP Standby Router for each VLAN with an STP priority one increment above the lowest priority.
2. Enable PortFast and BPDU Guard on all ports connected to end hosts (including WLC1). Perform the configurations in interface config mode.
## Part 5 – Static and Dynamic Routing
1. Configure OSPF on R1 (LAN-facing interfaces) and all Core and Distribution switches (all Layer-3 interfaces).
    - Use process ID 1 and Area 0.
    - Manually configure each device’s RID to match the loopback interface IP.
    - On switches, use the network command to match the exact IP address of each interface.
    - On R1, enable OSPF in interface config mode.
    - Make sure OSPF is enabled on all loopback interfaces, too. Loopback interfaces should be passive.
    - Each Distribution switch’s SVIs (except the Management VLAN SVI) should be passive, too.
    - Configure all physical connections between OSPF neighbors to use a network type that doesn’t elect a DR/BDR.
    - NOTE: This doesn’t work on the Layer-3 PortChannel interfaces between CSW1/CSW2. Leave them as the default network type.
2. Configure one static default route for each of R1’s Internet connections. They should be recursive routes.
    - Make the route via G0/1/0 a floating static route by configuring an AD value 1 greater than the default.
    - R1 should function as an OSPF ASBR, advertising its default route to other routers in the OSPF domain.

## Part 6 – Network Services: DHCP, DNS, NTP, SNMP, Syslog, FTP, SSH, NAT
1. Configure the following DHCP pools on R1 to make it serve as the DHCP server for hosts in Offices A and B. Exclude the first ten usable host addresses of each pool; they must not be leased to DHCP clients.
  - Pool: A-Mgmt
      - Subnet: 10.0.0.0/28
      - Default gateway: 10.0.0.1
      - Domain name: jeremysitlab.com
      -. DNS server: 10.5.0.4 (SRV1)
      - WLC: 10.0.0.7
- Pool: A-PC
    - Subnet: 10.1.0.0/24
    - Default gateway: 10.1.0.1
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
- Pool: A-Phone
    - Subnet: 10.2.0.0/24
    - Default gateway: 10.2.0.1
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
    - Pool: B-Mgmt
    - Subnet: 10.0.0.16/28
    - Default gateway: 10.0.0.17
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
    - WLC: 10.0.0.7
    - Pool: B-PC
    - Subnet: 10.3.0.0/24
    - Default gateway: 10.3.0.1
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
- Pool: B-Phone
    - Subnet: 10.4.0.0/24
    - Default gateway: 10.4.0.1
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
    - Pool: Wi-Fi
    - Subnet: 10.6.0.0/24
    - Default gateway: 10.6.0.1
    - Domain name: jeremysitlab.com
    - DNS server: 10.5.0.4 (SRV1)
2. Configure the Distribution switches to relay wired DHCP clients’ broadcast messages to R1’s Loopback0 IP address.
3. Configure the following DNS entries on SRV1:
    - google.com = 172.253.62.100
    - youtube.com = 152.250.31.93
    - jeremysitlab.com = 66.235.200.145
    - www.jeremysitlab.com = jeremysitlab.com
4. Configure all routers and switches to use domain name jeremysitlab.com and use SRV1 as their DNS server.
5. Configure NTP on R1:
    - Make R1 a stratum 5 NTP server.
    - R1 should learn the time from NTP server 216.239.35.0.
    - NOTE: NTP takes a LONG time to sync, especially in Packet Tracer. After making the configurations, you can move on – don’t wait for the devices to sync.
6. All Core, Distribution, and Access switches should use R1’s loopback interface as their NTP server. 
    - Clients should authenticate R1 using key number 1 and the password ccna.
7. Configure the SNMP community string SNMPSTRING on all routers and switches. The string should allow GET messages, but not SET messages.
8. Configure Syslog on all routers and switches:
    - Send Syslog messages to SRV1. Messages of all severity levels should be logged.
    - Enable logging to the buffer. Reserve 8192 bytes of memory for the buffer.
9. Use FTP on R1 to download a new IOS version from SRV1:
    - Configure R1’s default FTP credentials: username cisco, password cisco.
    - Use FTP to copy the file c2900-universalk9-mz.SPA.155-3.M4a.bin from SRV1 to R1’s flash drive.
    - Reboot R1 using the new IOS file, and then delete the old one from flash.
10. Configure SSH for secure remote access on all routers and switches.
    - Use the largest modulus size for the RSA keys.
    - Allow SSHv2 connections only.
    - Create standard ACL 1, only allowing packets sourced from Office A’s PCs subnet. Apply the ACL to all VTY lines to restrict SSH access.
    - Allow only SSH connections to the VTY lines.
    - Require users to log in with a local user account when connecting via SSH.
    - Configure synchronous logging on the VTY lines.
11. Configure static NAT on R1 to enable hosts on the Internet to access SRV1 via the IP address 203.0.113.113.
12. Configure pool-based dynamic PAT on R1 to enable hosts in the Office A PCs, Office A Phones, Office B PCs, Office B Phones, and Wi-Fi subnets to access the Internet.
- Use standard ACL 2 to define the appropriate inside local address ranges in the following order:
    - Office A PCs: 10.1.0.0/24
    - Office A Phones: 10.2.0.0/24
    - Office B PCs: 10.3.0.0/24
    - Office B Phones: 10.4.0.0/24
    - Wi-Fi: 10.6.0.0/24
- Define a range of inside global addresses called POOL1, specifying the range 203.0.113.200 to 203.0.113.207 with a /29 netmask.
- Map ACL 2 to POOL1 and enable PAT. Confirm that hosts can access the Internet by pinging jeremysitlab.com.
- Verify that Internet link failover works by disabling R1’s G0/0/0 interface and pinging again.
- You will need to remove and re-configure the OSPF default-information originate command for this to work. In real Cisco routers, you can configure the default-information originate always command that supports failover like this, but the command isn’t available in Packet Tracer.
- Re-enable G0/0/0 (and remove and re-configure default-information originate once again).
13. Disable CDP on all devices and enable LLDP instead. 
- Disable LLDP Tx on each Access switch’s access port (F0/1).

## Part 7 – Security: ACLs and Layer-2 Security Features
1. Configure extended ACL OfficeA_to_OfficeB where appropriate:
    - Allow ICMP messages from the Office A PCs subnet to the Office B PCs subnet.
    - Block all other traffic from the Office A PCs subnet to the Office B PCs subnet.
    - Allow all other traffic.
    - Apply the ACL according to general best practice for extended ACLs.
2. Configure Port Security on each Access switch's F0/1 port:
    - Allow the minimum necessary number of MAC addresses on each port.
    - SRV1 does not use virtualization, so it uses a single MAC address.
    - Configure a violation mode that blocks invalid traffic without affecting valid traffic. The switches should send notifications when invalid traffic is detected.
    - Switches should automatically save the secure MAC addresses they learn to the running-config.
3. Configure DHCP Snooping on all Access switches.
    - Enable it for all active VLANs in each LAN.
    - Trust the appropriate ports.
    - Disable insertion of DHCP Option 82.
    - Set a DHCP rate limit of 15 pps on active untrusted ports.
    - Set a higher limit (100 pps) on ASW-A1’s connection to WLC1.
4. Configure DAI on all Access switches.
    - Enable it for all active VLANs in each LAN.
    - Trust the appropriate ports.
    - Enable all optional validation checks.

## Part 8 – IPv6
1. To prepare for a migration to IPv6, enable IPv6 routing and configure IPv6 addresses on R1, CSW1, and CSW2:
    - R1 G0/0/0: 2001:db8:a::2/64
    - R1 G0/1/0: 2001:db8:b::2/64
    - R1 G0/0 and CSW1 G1/0/1: Use prefix 2001:db8:a1::/64 and EUI-64 to generate an interface ID for each interface.
    - R1 G0/1 and CSW2 G1/0/1: Use prefix 2001:db8:a2::/64 and EUI-64 to generate an interface ID for each interface.
    - CSW1 Po1 and CSW2 Po1: Enable IPv6 without using the ‘ipv6 address’ command.
2. Configure two default static routes on R1:
    - A recursive route via next hop 2001:db8:a::1.
    - A fully-specified route via next hop 2001:db8:b::1. Make it a floating route by configuring the AD 1 higher than default.

## Part 9 – Wireless
1. Access the GUI of WLC1 (https://10.0.0.7) from one of the PCs.
    - Username: admin
    - Password: adminPW12
2. Configure a dynamic interface for the Wi-Fi WLAN (10.6.0.0/24)
    - Name: Wi-Fi
    - VLAN: 40
    - Port number: 1
    - IP address: .4 of its subnet
    - Gateway: .1 of its subnet
    - DHCP server: 10.0.0.76
3. Configure and enable the following WLAN:
    - Profile name: Wi-Fi
    - SSID: Wi-Fi
    - ID: 1
    - Status: Enabled
    - Security: WPA2 Policy with AES encryption, PSK of cisco123
4. Verify that both LWAPs have associated with WLC1.
    - Due to Packet Tracer’s limitations, wireless clients won’t be able to lease an IP address from the Wi-Fi DHCP pool.

