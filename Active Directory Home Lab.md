# *Active Directory Lab*
**Date**: 7/15/2026

**Software & Tools** : Windows Server 2025, Windows 11, Oracle VirtualBox.
## *Objective* 
Create a lab enviornment using VirtualBox with a Windows Server domain controller and a Windows client. The goal being to practice common help desk tasks — configuring DHCP and DNS, joining a client to the domain, and managing users, groups, and Group Policy — and troubleshoot real issues along the way.

### ***Prerequisites*** 
- Download Oracle Virtualbox
- Download Windows Server 2025 ISO
- Download Windows 11 ISO
- Host Machine that can run two or more VM's simultaniously
## *Steps*
- Create a Virtual Machine (VM) with the necessary hardware requirements to run Windows Server 2025. Go to Expert settings for the VM and enable two network adapters, one NAT and the other Internal. Install and set up the Server OS on the VM.
- Before installing directory roles, go to Network connections on the server VM. Right-click the internal adapter, select Properties, then IPv4. Set up a static IP by selecting "Use the following IP address," and plug in the following network values:

*IP Address*: 10.10.10.1

*Subnet Mask*: 255.255.255.0

*Preferred DNS Server*: 127.0.0.1 (loopback address — this works because the DNS role gets installed automatically once you promote the server to a domain controller)
- **Install Active Directory Domain Services**. Go to Add Roles and Features, and select Active Directory Domain Services. Click next until you reach Install, then install. After installation, click the flag alert next to Manage to promote the server to Domain Controller. Select Add a new forest. After naming the server and creating a password, the VM should restart.
- **Add a DHCP server**. Add a DHCP server. Go to Add Roles and Features, select DHCP Server, and install. Once it's installed, right-click the server in the DHCP console and Authorize it — skip this and clients won't be able to pull an address from it. Then set a New Scope by right-clicking the IPv4 server under DHCP. Make the *start IP* 10.10.10.100 and the *end IP* 10.10.10.200.
- **Create Users**. Go to Tools (top-right), AD Users and Computers. Expand the folders, right-click Users, then click New. Set up easy passwords and make it so user passwords don't expire, since this is just for the lab environment.
- **Create a Windows 11 Pro VM**. Make sure to enable two adapters on this VM, one internal and the other NAT. This VM will act as our client PC connecting to the domain over a LAN connection.
- Ping 10.10.10.1 to confirm connectivity to the DC. After the client is connected to the network, join the client to the domain. Go to Settings, Accounts, Access work or school, Join this device to a local Active Directory domain, and enter the domain name. Enter the domain admin credentials when prompted. After joining, try signing into one of the users that were previously created to test.
- At this point the lab is ready for experimentation. Disable accounts, change passwords, and mess with user log on times.
