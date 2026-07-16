# *Active Directory Lab*
**Date**: 7/15/2026

**Software & Tools** : Windows Server 2025, Windows 11, Oracle VirtualBox.
## *Objective* 
Create a lab enviornment using VirtualBox with a Windows Server domain controller and a Windows client. The goal being to practice common help desk tasks — configuring DHCP and DNS, joining a client to the domain, and managing users, groups, and Group Policy — and troubleshoot real issues along the way.

### ***Prerequisites*** 
- Download Oracle Virtualbox
- Download Windows Server 2025 ISO
- Download Windows 11 ISO
## *Steps*
- Create a Virtual Machine (VM) with the necessary hardware requirements to run windows server 2025. Go to Expert settings for the VM and enable two network adapters one NAT and the other Internal. Install and setup the Server OS on the VM.
- Before installing directory roles go to Network connections on the server VM. Right-click the internal adapter, select properties, then IPv4. Setup a static IP by selecting "Use the following ip address", Plug in the following network values:

    IP Address:  10.10.10.1

    Subnet Mask: 255.255.255.0 

    Preferred DNS Server:  10.10.10.1 OR 127.0.0.1 (loopback address)
- Install Active Directory Domain Services. Go to Add roles and Features, and select Active Directory Domain Services. Click next until you reach install then install, after installation click the flag alert next to manage, to promote the server to Domain Controller. Select add a new forest. After nameing the server and creating a password the VM should restart.
- Add a DHCP server. Go to Add roles and features, DHCP server and install. After the installation configure set a New Scope by right clicking on server. Make the start IP 10.10.10.100 and the end IP 10.10.10.200.
- Create Users. Go to Tools (top-right), AD Users and Computers, Expand folders and right click users, then click new. Set up easy passwords and make it so user passwords dont expire for the lab enviornment.
- Create another VM and install windows 11 pro on it, also make sure two enable to adpaters on this vm as well.One adapter will be internal and the other NAT. This VM will act as our client PC. Setup network adapter as internal adn allow vm's. go to network connections and assign a static ip to the client adapter.

   IP Address: 10.10.10.2

   Subnet Mask: 255.255.255.0
  
   Preferred DNS Server: 10.10.10.1

- Run ipconfig to confirm the client's static IP was applied correctly, then ping 10.10.10.1 to confirm connectivity to the DC. After the client is connected to the network join the client to the domain. Go to Settings, Accounts, Access work or school, Join this device to a local Active Directory domain, enter the domain name. Enter in the domain admin credentials when prompted. After joining try signing into one the users that were previously created to test. Try disabling users and changing passwords.
