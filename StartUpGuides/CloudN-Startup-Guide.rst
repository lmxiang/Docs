
|image0|

========================
 Virtual Appliance CloudN Startup Guide
========================

 Version 05-23-2017

 Copyright © 2014-2017 Aviatrix Systems, Inc. All rights reserved.




Welcome
=======

This is a startup guide for the initial installation. CloudN is simple
to install and easy to use. If you are a first time user, this document
is for you.

There is no separate document as user guide, explanations on how to use
CloudN is embedded in the CloudN console. You can also find useful
information on Frequently Asked Questions (FAQs) at the Help tab on the
console.

In this guide, the terms VPC/VNet Container, Container and VPC/VNet may
be used interchangeably. In general, a Container is a fully populated
AWS VPC or Azure VNet with all resources and encrypted tunnel
established. When a VPC/VNet Container is created, users are ready to
launch instances/VMs in the VPC/VNet and accessing them using their
private IP addresses as if they are in the on-prem network.

CloudN supports REST API that allows third party software integration.
REST API document can be found at CloudN console Help menu.

CloudN Benefits
===============

CloudN is a single platform that supports both Amazon AWS and Microsoft
Azure. It dynamically creates VPC/VNet and securely connected them to
enterprise network in a few minutes of time. Each VPC/VNet is fully
populated with network infrastructure resources such as private and
public subnets, routing and security policies. You may use CloudN for
distributed application deployment in the cloud in multiple regions; let
a developer launch a IT managed sandbox; give a business unit or
department their own VPC; replace your existing AWS VGW based VPN
solutions; connect partners in the cloud, and more, as illustrated in
the diagram below.

|image1|

Key feature list on CloudN:
---------------------------

Deployment

-  Deployed anywhere within your datacenter. No need to touch network
   infrastructure.

-  No additional public IP address needed.

-  Easy onboarding process takes a few minutes to complete.

-  Seamless, transparent and secure by-direction traffic flow between
   all instances/VMs in a VPC/VNet and on-prem resources.

-  Time Service to allow CloudN VM sync to a specified NTP time server.

-  Periodic system configuration backup to AWS S3.

-  Support Rest API for third party integration and automation.

-  Floating license scheme allows license sharing among multiple CloudN
   deployment.

-  Runs on VMware and Microsoft Hyper-V hypervisors, Virtual Box, VMware
   Fusion, VMware Workstation

-  Can be deployed as both a virtual appliance and dedicated hardware
   appliance.

VPC/VNet Features

-  Dynamically create a VPC with secure connectivity to data center in a
   few minutes.

-  Rapid scaling to multiple VPC/VNets.

-  Encrypted VPC/VNet peering between VPC/VNets in the same and
   different regions and across clouds.

-  Native AWS VPC peering in the same region.

-  Redundant cloud gateway for high availability support.

-  Support ESXi based vmware High Availability (HA) and Fault Tolerance
   (FT) on local CloudN controller.

-  Security policies at the VPC/VNet level with fine granular rules.

-  Integrate NAT function for direct Internet access for instances
   inside a VPC/VNet.

-  Support remote workers and off premise direct secure connectivity to
   VPC/VNet via OpenVPN Client.

-  LDAP/AD integration with OpenVPN for user authentication.

-  Support additional multi factor authentication: Google 2-step, DUO
   security and OKTA.

-  Support user profile defined access policy for a dynamic access
   control to cloud resources.

-  Replace legacy VPC AWS VGW based VPN solution with CloudN for a
   central point of control and management.

-  Connect to existing (legacy) VPC for peering with any CloudN
   controlled VPC/VNets.

-  Support add-on OpenVPN remote access on a legacy VPC for remote
   workers.

-  Deployed in branch offices or remote data centers to allow direct
   secure connectivity to VPC/VNet without backhauling traffic to
   datacenter.

Instance Features

-  Support instance profiling to create template for launching instance
   from CloudN console.

-  Support customer CloudFormation scripts integration for AWS.

IT Managed Self-Service

-  Support multiple AWS accounts or IAM accounts.

-  Support Role Based Access Control (RBAC) between Admin account and
   CloudN cloud account.

-  Support multiple users in Admin account and each cloud account.

-  Support 2FA authentication for the console login.

-  Email notification for account creation, VPC creation/deletion and
   OpenVPN user creation for streamline operation.

Monitoring and Troubleshooting

-  Real time VPC secure tunnel state monitoring.

-  Real time and historic traffic statistics displaying bandwidth
   consumption on a per VPC/VNet bases.

-  Cost monitoring through billing alert for a CloudN user account in
   AWS.

-  Support CloudTrail and Splunk integration per CloudN account for AWS
   API logging.

-  Support Splunk logging for CloudN API.

-  Support Splunk and logstash forwarder for VPC/VNet user traffic.

-  Monitoring and alert any stopped instances and unassociated EIP to
   reduce costs in AWS.

-  Ping, packet capturing and extensive trace log facilitate debugging
   and troubleshooting.

How It Works
============

(It is not necessary to understand how CloudN works completely in order
to use it. It is OK if you like to skip this section.)

Mix Layer 2 and Layer 3 Technologies
------------------------------------

Cloud Enabler or CloudN is an appliance that can be deployed anywhere
within your enterprise network. It is used by enterprises to create
VPC/VNets and securely connect to them from the enterprise network.
Following is a diagram of deploying a CloudN in your enterprise
datacenter.

|image2|

*Figure 1: CloudN Deployment Diagram*

CloudN uses a mixed Layer 2 and Layer 3 technologies whereas the
CloudN-local behaves as a Layer 2 bridge and CloudN-remote (launched by
CloudN-local at VPC/VNet creation time) behaves as a Layer 3 router. The
design of CloudN-local as a Layer 2 bridge makes it possible to build an
overlay IPSec tunnel to CloudN-remote without involving edge routers in
the network. The design of CloudN-remote as a Layer 3 router makes it
possible for the Container to fully utilize all AWS VPC underlying
infrastructures and services without requiring any software agent reside
in any of the instances.

Instances within the VPC/VNet communicate with each other directly and
transparently without involvement of CloudN-remote. In addition, VMs
within an Azure VNet communicate with each other directly or through
CloudN-remote. Accessing instances in the VPC/VNet from on-prem is also
seamless. From the user’s perspective, what CloudN creates is a standard
VPC/VNet.

With CloudN you can create a VPC/VNet dynamically and on demand in a few
minutes of time.

You can now run an application or product in its own Container,
resulting in a more secure environment than on premise datacenter by
isolation applications from each other.

CloudN views each VPC/VNet as the smallest autonomous environment, it
allows you to create security policies to deny any subnet or hosts on
premise to access any VPC/VNet. For example, you may want to block
developers from accessing production VPC/VNet. By default,
inter-VPC/VNet communication is blocked. By using VPC/VNet peering
capability, you can establish direct secure tunnels among VPC/VNets in
the same region or across different regions.

A VPC/VNet Container is a VPC/VNet, with (optional) public subnet and
private subnet in each availability zone, AWS Internet Gateway (IGW),
routing and CloudN-remote gateway. At the creation time you can also
specify security policies stored in AWS S3 as CloudFormation Scripts.
Secure tunnels are automatically established to each Container at
creation time.

Enterprise users can access instances seamlessly in all private and
public subnets over the secure tunnel using instance private addresses.
All instances on private subnets can reach back to enterprise.
Optionally packets from instances on private subnets can reach Internet
directly without being first sent back to the enterprise.

Dividing Subnets
----------------

CloudN works by dividing the subnet where cloudN is deployed into sub
segments (or smaller subnets). The VPC CIDRs created by cloudN are one
of the sub segments. The mechanism is illustrated below. VPC in the
below diagram could be replaced with a VNet.

|image3|

*Figure 2: Dividing Subnets*

Where a local subnet 10.16.0.0/16 has a default gateway 10.16.0.1. The
subnet is divided into 4 sub segments. The default gateway and CloudN IP
address fall into one segment. The rest of each segment is mapped to a
VPC CIDR, in this case, the VPC CIDRs are 10.16.32.0/19, 10.16.64.0/19
and 10.16.96.0/19. If this subnet 10.16.0.0/16 is reachable from other
network in the enterprise, then the instances inside each VPC takes
private IP address as if they are on the local subnet 10.16.0.0/16. For
users in the enterprise, it is as if they are communicating with hosts
on the local network.

The same mechanism is applied to Azure to create VNets.

Pre-Installation Check List
===========================

AWS EC2 Account
---------------

If you intend to launch VPC in AWS, you need to have an AWS account.

You need to have an AWS account in order to use most of the commands on
CloudN. Note that CloudN support multiple CloudN cloud accounts with
each one associated with a different AWS account or IAM account, but
there needs to be at least one to start with.

The AWS account can be a root account, an IAM user in Administrator
Group or an IAM user with full access permission to EC2, VPC, S3, SQS,
SNS, CloudTrail and Route 53. For security reasons, we strongly
recommend you use IAM user account. During onboarding, you will have
opportunity to copy and paste a custom policy required by Aviatrix to
your AWS IAM account.

IAM Administrator
-------------------

The following steps show you how to add a user to Administrator Group in
AWS.

Step 1. Login to https://console.aws.amazon.com/iam

Step 2. Click Users, select the user that needs to be added to
Administrative privilege, click Add User to Groups

|image4|

Step 3. Add joe\_smith to admin group which was created previously via
Groups tab on the console.

|image5|

IAM User
---------

If you are an IAM user, make sure you have full access to EC2, VPC, S3,
SQS, SNS and CloudTrail service. Refer to this link on how to setup an
IAM access policy required by CloudN. During the onboarding process, we
will guide you through on setting up this IAM customer policy.

Microsoft Azure Account
-----------------------

If you intend to create VNets in Microsoft Azure, you need to create an
Azure account. If not, you can skip this step.

Deployment Positions
--------------------

You need to identify or create a subnet where CloudN is deployed. CloudN
is deployed on a private subnet anywhere on your network. CloudN does
not take a public IP address. Make sure this subnet is reachable by
other subnets where traffic is originated from.

CloudN should be deployed on a subnet (or VLAN) where CloudN is the only
virtual machine on the VLAN. CloudN VM’s IP address is determined by
CloudN software during installation time.

The default gateway for the VLAN should either have the lowest address
or highest address for the VLAN. For example, if the VLAN where CloudN
is deployed is 10.10.0.0/16, the default gateway IP address for this
VLAN should be either 10.10.0.1 or 10.10.255.254.

The size of this subnet or VLAN should be large enough to allow the
creation of the desired number of VPCs. For example, a network with /16
prefix can support 15 VPC/VNets with each VPC/VNet contains /24 subnet
in AWS or Azure.

CloudN allocates 4 bits or 16 subnets in each VPC. By default, two
subnets, one private and one public subnets are created in each
available zone. A user can customize and create additional subnets.

Deploy on Subnets larger than /24
----------------------------------

If you deploy a CloudN in a /23 subnet, only two VPC/VNet can be
created. This VPC/VNet can support 8 subnets.

It is recommended that you deploy CloudN in a subnet size between /16
and /22. Below is the table that describes the subnet size and the
maximum number of VPCs.

|image6|

Deploy on a Class C Subnet
--------------------------

Deploying CloudN in a /24 subnet is a special case. It is handled
differently from any other size of subnets.

In this case, there is only one public subnet and 2 private subnets with
each in a different availability zone created for a VPC Container. Up to
3 VPCs can be launched. Since not every AZ (Availability Zone) is
covered in subnet creation, applications that require subnets in each AZ
would not work. Deploying on /24 subnet is best used for POC projects.

If you have local machines on the subnet where CloudN is deployed, you
need to make sure all local machines including the default gateway and
CloudN are in one sub segmented area, as illustrated below:

|image7|

*Figure 3: Class C Subnet Deployment*

Leaving local machines outside the address range of 192.168.1.0/26 can
result in duplicate IP addresses.

Each VPC has 1 public subnet and 2 private subnets.

Deploy CloudN in remote sites
-----------------------------

You can deploy CloudN in a remote site to allow the remote site network
to connect securely and directly to a VPC created by the main datacenter
deployed cloudN, as shown below.

|image8|

In this deployment, CloudN functions as a router. It is not required
that CloudN is deployed in large subnet segment, it is not even required
that CloudN is deployed in a subnet of its own. What is required is that
the default gateway of the subnet where CloudN is deployed has a static
route configured that routes traffic destined to the VPC CIDR where this
remote site wish to connect to the CloudN.

Network Interfaces
------------------

CloudN local gateway is installed as a VM host with two network
interfaces. Make sure the two interfaces are on the same VLAN or subnet.

If CloudN runs on a VMware Workstation, VMware Fusion or VMware Player,
you do not need to configure the network interfaces as they are
pre-configured as part of OVF image, unless you are installing them in
NAT mode subnet (in which case make sure both Network Adapters are in
NAT mode)

If CloudN runs on VMware ESXi host, follow the instruction in the next
chapter to enable promiscuous mode and forged transmit mode for both
interfaces.

If CloudN runs on Microsoft Hyper-V, you do not need to configure the
network interfaces as they are pre-configured as part of VHD image. Make
sure that “Enable MAC Address Spoofing” is enabled (explained in the
installation section)

If CloudN runs on VirtualBox, both network interfaces need to be in
bridge mode. Instructions to do this are available in section 5.7.2

Internet Connectivity
---------------------

CloudN needs to have Internet connectivity to perform most its
functions.

Proxy Settings
--------------

If there is proxy server on-prem for Internet access, contact IT
administrator to obtain proxy server IP address, proxy port, and if
there needs to have username and password for authenticating by the
proxy.

Binding to CloudN Private IP address to a Single NAT Public IP Address
----------------------------------------------------------------------

If your organization has more than one public IP addresses as the NAT
address, you must bind CloudN’s private IP address to one of the public
IP addresses. That is, CloudN will always be translated to one static
public IP address for its outbound traffic.

For example, on Cisco ASA, you can configure the following to bind a
private IP address to one public IP:

Step 1  Create a network object for the internal servers.

::

   hostname(config)# object network myWebServ

   hostname(config-network-object)# range 10.1.1.1 10.1.1.70

Step 2  Configure NAT to map servers from 10.1.1.1 to 10.1.1.70 to a
static public IP (209.165.201.10)

::

  hostname(config-network-object)# nat (inside,outside) static 209.165.201.10

Outbound TCP/UDP Ports
----------------------

CloudN requires the following TCP/UDP outbound ports open.

-  TCP port 443 for all AWS public IP address ranges.

-  UDP ports 4500 and 500 for all AWS public IP address ranges.

   If you choose to reduce the scope of above ports, you can limit them
   to only AWS owned public IP address blocks.

Since CloudN operates in a client-server mode where the CloudN local
gateway is the client, there is no restriction or requirement to open
any known TCP/UDP port for inbound traffic.

Time Service
------------

CloudN uses extensively Amazon Web Service (AWS) APIs and Azure REST
APIs. These APIs checks timestamp for each API call. CloudN is
pre-configured to synchronize its time with Host (please double check on
the VM advanced option to make sure this is the case.) To ensure correct
operation of CloudN, it is important that the Host where CloudN is
installed has correct time.

Most likely enterprise data center syncs VM time to host. However if
your environment requires you to sync time to an NTP server, CloudN
allows you to accomplish that. You can configure this at Settings ->
Time Service.

Performance Consideration
-------------------------

CloudN is a virtual appliance that runs on a hypervisor. The supported
hypervisors are VMware hypervisor products, Microsoft Enterprise 8.1
Hyper-V and Oracle VirtualBox.

By default CloudN is packaged with 2 vCPU and 4GB of memory as part of
its image make up. You can always reconfigure the VM to take more CPU
and memory.

For maximum performance, it is recommended that the host CPU has support
for Intel AES-NI, instruction set for hardware encryption. Intel
processors Westmere, Sandybridge, Ivrybridge and Haswell all have AES-NI
enabled.

In test environments, TCP throughput (using iperf tool) in the vicinity
of 880Mbps has been observed with CloudN running on a VMware ESXi host
with an Intel Xeon CPU (E3-1220L V2 @ 2.30GHz).

Installation
============

Download CloudN Images
----------------------

CloudN comes with two types of images, OVF and VHD, to support VMware
hypervisor and Microsoft Hyper-V.

CloudN OVF image can be imported and installed on a VMware ESXi 5.0/5.1
host, VMware Workstation, Fusion and VMware Player. Once you have signed
up as a Aviatrix customer, follow the instructions to download the zip
file on your PC. CloudN OVF image usually takes the name
“cloudN-ovf-date” where date is the time when the image was built.

CloudN is recommended to run on ESXi 5.0 or later version. However you
can install the software on VMware Player, VMware Workstation and Fusion
for testing and evaluation purposes.

Installation on ESXi 5.0 or later
---------------------------------

After downloading and extracting the zip file, copy the folder to a
location where you can import the virtual machine. For installation,
follow the steps below.

Step 1: In the vSphere Client, select File > Deploy OVF Template

|image9|

Step 2: Locate the folder where “.ovf” file is located

|image10|

Step 3: Click Next to proceed through the rest of the installation.
Please refer to the page
`ESXi Admin <https://pubs.vmware.com/vsphere-51/index.jsp?topic=%2Fcom.vmware.vsphere.vm\_admin.doc%2FGUID-6C847F77-8CB2-4187-BD7F-E7D3D5BD897B.html>`_
for more detailed instructions.

Configure Network Adapter Properties
-------------------------------------

CloudN has two network interfaces, both of them need to be on the same
VLAN.

After the installation is finished, follow these steps to enable
promiscuous mode on the network adapter (below is an example):

Step 1. Select (Highlight) ESXi host tab where CloudN is hosted (for
example, 192.168.1.34) and click on the Configuration tab

|image11|

Step 2. In the Hardware section, click Networking and then properties

|image12|

Step 3. Select VM Network adapter for CloudN and click edit

|image13|

Step 4. Click the Security tab, from the Promiscuous Mode dropdown menu,
click the box and select accept and click OK. If you are running ESXi
5.1 or later, you also need to set Forged Transmit Mode for the port
group to “Accepted”.

|image14|

For more information on configuring security policies on the network
switch, please refer to the instructions in `this link <http://pubs.vmware.com/vsphere-51/index.jsp?topic=%2Fcom.vmware.vsphere.networking.doc%2FGUID-74E2059A-CC5E-4B06-81B5-3881C80E46CE.html>`_.

For additional CloudN on ESXi configuration illustrations, check out
`this note <https://s3-us-west-2.amazonaws.com/aviatrix-download/Cloud-Controller/Configuring_CloudN_Examples.pdf>`_

Special Notes
----------------

CloudN does not support NICteaming in active-active mode. When
NICteaming is configured, only active-standby mode is supported, as
shown below where the ESXi host has 4 Ethernet ports and VLAN220 is the
port group CloudN Ethernet ports belong to.

|image15|

Note that CloudN currently does not support vMotion.

Installation on Windows 8.1 Enterprise Edition
----------------------------------------------

CloudN VHD image can be deployed on Windows 8.1 Enterprise Edition, or
Windows 2012 Server R2 Hyper-V.

After downloading the zip file and decompressing it, copy the folder to
a location where you can import the virtual machine. For installation,
follow guide below.

Step 1: Import the VHD Image

|image16|

Step 2: Locate Folder

|image17|

Step 3: Copy the Virtual Machine

|image18|

Step 4: Connect to the Virtual Machine

|image19|

Step 5: Start the Virtual Machine

|image20|

Step 6: Login into Virtual Machine

::

  User Name: admin

  Password: Aviatrix123#

Enable MAC Address Spoofing
----------------------------

Both Network Adapters associated with CloudN VM should have “Enable MAC
Address Spoofing” turn on. This is accomplished by expand Network
Adapter, select Advanced Feature and check the box “Check MAC Address
Spoofing”, for each Network Adapter.

As part of VHD image, this setting should already be configured and
should not be changed.

|image21|

NIC Teaming Support
-------------------

NIC teaming is only supported for active standby mode.

Running CloudN on Wireless Host
---------------------------------

CloudN VHD image is packaged with its virtual switch configured with
External Network Wire. If your host machine has wireless network
adapter, you need to change the binding of virtual switch to External
Network Wireless. Highlight the VM, choose settings, choose Network
Adapters and configure as shown in the picture below.

|image22|

Test Drive on Your Laptop
-------------------------

CloudN can be installed on your laptop or desktop running on VMware
Workstation, Fusion and Windows Enterprise 8.1 in NAT mode. You can use
this deployment for testing and evaluation purpose.

Installation on VMware Workstation is straight forward. Use “Open”
option to import the OVF file.

Test Drive CloudN in NAT Mode or Hyper-V Internal Network Wire Mode
---------------------------------------------------------------------

One good configuration to test drive cloudN is to deploy it on your
laptop on a private subnet in NAT mode (In Hyper-V, the network adapters
are configured as Internal Network Wire). However, since VMware
Workstation and Fusion allows only one NAT mode subnet, special
attention must be given if you have other VMs that shares the subnet.
Sharing subnet or VLAN with other VMs is not a recommended model in real
production deployment.

As an example, if your NAT mode subnet is 192.168.10.0/24, you can
create a maximum 2 VPCs from CloudN deployed on this subnet. Suppose the
default gateway IP address is 192.168.10.2. CloudN will automatically
take 192.168.10.3 as its IP address. In addition CloudN reserves IP
address ranges from 192.168.10.4 to 192.168.10.7. If you have other VMs
running on this subnet, make sure their IP address fall in the same sub
segment as CloudN but not overlap with CloudN and its reserved address
range. Once you launch VPCs from this CloudN, the other VMs on the
subnet should be able to run SSH, RDP, and SCP (file copy) to any
instances in VPCs using the instance private IP address seamlessly,
without any bastion station or landing VPC. Refer to How It Works
section for more explanations.

If you install CloudN on a NAT subnet, make sure both Ethernet
interfaces are changed to NAT mode (By default, CloudN is pre-configured
and shipped with both Network Adapters in Bridged mode). Right click on
the CloudN VM, click Settings. Change both Network Adapters to NAT mode,
as shown below for VMware Workstation:

|image23|

Test Drive on MAC with vmware Fusion
------------------------------------

After downloading the zip file and decompressing it, copy the folder to
a location, where your Mac can access it. Perform the following steps to
install CloudN.

Step 1: From the VMware Fusion menu bar, select File > Import.

|image24|

Step 2: The Import Library window appears, along with a dialog box for
browsing to the location of OVF file.

|image25|

Step 3: Browse to the .ovf file and click open

|image26|

Step 4: Type the name for the imported virtual machine in the Save
As text box and indicate where to save it.

|image27|

Step 5: After the import is complete, the virtual machine appears in the
virtual machine library. Click on “Start Up” to start the CloudN virtual
machine.

|image28|

Step 6: Change Network Adapters to NAT mode

Select the VM, click Settings, click Network Adapter, select “\ **Share
with my Mac**\ ”, as shown below

|image29|

Test Drive on PC with VMware Workstation
-----------------------------------------

Click on File -> Open, as shown below.

|image30|

Then open the desired VM.

|image31|

Highlight the VM, right click, select Settings, click on Network
Adapter, change both Network Adapter to NAT mode as shown below.

|image32|

Test Drive on VirtualBox
------------------------

CloudN works on VirtualBox only in a bridged mode.

After downloading and extracting the zip file, copy the folder to a
location where you can import the virtual machine. For installation,
follow the steps below.

Installation
=============

Step 1: From the VirtualBox menu bar, select File > Import Appliance

|image33|

Step 2: Navigate to the CloudN ovf file and click “Next”

|image34|

Step 3: In the next screen, click on “Import” to start the import
process and wait for it to finish

|image35|

Step 4: CloudN virtual machine installation is finished and it can be
launched by selecting it and clicking on the “Start” button.

|image36|

Configure Network Interfaces
----------------------------

CloudN network interfaces should be configured in bridge mode as the NAT
mode makes it impossible for guests to communicate with each other. In
addition to this, both interfaces should be allowed to be in promiscuous
mode. Execute the steps below to satisfy these requirements.

Step 1: Select the CloudN VM and click on “Settings”

|image37|

Step 2: In the settings window, select “Network” and select "Bridged
Adapter" in the drop down list for the "Attached to" field.

|image38|

Step 3: Click on “Advanced” to reveal advanced configuration options and
select “Allow All” in the drop down list for “Promiscuous Mode” field.
Repeat this procedure for “Adapter 2” as well.

|image39|

Booting Up and Initial Configuration
====================================

CloudN supports browser based GUI Interface and REST APIs.

After the virtual machine boots up, you must first login into the
machine while still in hypervisor console.

**CloudN Login User Name: admin**

**CloudN Login Password: Aviatrix123#**

After this initial login, if you see the screen the screen below.

|image40|

Follow the instruction to type “help” at the prompt.

|image41|

Follow the steps to go through the boot up process. You can type “help”
at any time to review the steps. Type “?” to view all available
commands. For each command, type “?” to view syntax and parameters.

Step 1: Setup Interface Address
-------------------------------

CloudN works by dividing the subnet where CloudN is deployed into
sub-segment where each sub-segment becomes the VPC/VNet CIDR in the
cloud. We recommend you deploy CloudN in its own subnet to maximize the
number of VPC/VNets you can create.

There are two ways to give CloudN its IP adddress: auto-generate by
CloudN itself or statically assign one.

Statically assign CloudN IP address
------------------------------------

You can statically assign an IP address to CloudN. Choose this approach
if you use CloudN to connect to an existing VPC. In the use case where
CloudN does not create a VPC and build encrypted tunnel, CloudN does not
need to be deployed on a separate subnet.

Command: setup\_interface\_static\_address

Syntax: setup\_interface\_static\_address [static\_ip\_address]
[net\_mask] [default\_gateway\_ip\_address]
[primary\_dns\_server\_ip\_address]
[secondary\_dns\_server\_ip\_address] [proxy {true\|false}]

Below is an example where there is no proxy server. In such case, CloudN
will configure the network interfaces, test Internet connectivity and
download the latest Aviatrix software.

|image42|

Proxy Configuration
--------------------

If there is proxy server for Internet access, you must setup proxy
configuration on CloudN to pass traffic to proxy correctly. Following is
the command

command: setup\_network\_proxy

syntax: setup\_network\_proxy <action> <--http\_proxy> <--https\_proxy>

where action is “test” or “save”.

Example:

::

  setup\_network\_proxy test --http\_proxy http://10.30.0.3:3128
  --https\_proxy http://10.30.0.3:3128

  setup\_network\_proxy save --http\_proxy http://10.30.0.3:3128
  --https\_proxy http://10.30.0.3:3128

Note after proxy configuration is saved, CloudN VM will reboot to have
the proxy take effect.

Auto-generate CloudN interface IP address
-----------------------------------------

All you need to do here is to provide information related to the subnet
where CloudN is deployed. CloudN scans the subnet and find an IP address
that is close to the default gateway (for example, if the default
gateway is 10.10.0.1, CloudN will try 10.10.0.2) and is available,
CloudN will then assin itself this IP addres and CloudN software will be
downloaded if configuration is successfully.

Command setup\_interface\_address:

Syntax: setup\_interface\_address [net\_mask]
[default\_gateway\_ip\_address] [dns\_server\_ip\_address\_1]
[dns\_server\_ip\_address\_2] [proxy {true\|false}]

|image43|

CloudN will identify an unused IP address in an iterative fashion and
assign it to itself. As seen in the above example, the IP address
generated is 10.88.0.3.

Once the IP address is generated, CloudN will start to download the
latest CloudN software.

…….. snippet…….

|image44|

If you see the above message, the download is completed.

Step 2: Display Interface Address
---------------------------------

|image45|

Now you can use the cloudN IP address as URL to access CloudN Manager
that manages CloudN.

Note: The hypervisor console has only limited CLI for initial booting up
purposes. Once Aviatrix software is downloaded, full commands are
installed.

User should use the GUI to access CloudN Console.

Troubleshooting
---------------

If there is any error messages during installation, it is usually due to
lack of Internet connectivity, incorrect DNS server IP address or
unopened firewall ports. Type “?” to see all the commands that help you
troubleshoot.

Use command “\ ***ping***\ ” and “\ ***traceroute***\ ” to check out
Internet connectivity. Check your DNS server setting, consult your
network and server admin to determine the cause of routing failure.

After connectivity issue is resolved, use command
“download\_cloudn\_software” to continue installation and finish. Or you
can again type in command setup\_interface\_address.

Use a Browser to Access CloudN
------------------------------

CloudN has a built in CloudN Console that let you run provisioning from
a browser.

Once IP addressed setup is complete, you can use any browser, type
https://<IP address of CloudN> and see a Login page.

|image46|

Login with:

User Name: **admin**

Password: **private IP address of the VM**

After login, go through the initial setup process.

For the first time user and initial setup, follow Onboarding to go
through the initial set up and launch your first VPC/VNet.

Onboarding
==========

After you login to the browser console, click Onboarding to go through a
few steps of initial setup and start creating the first VPC/VNet.

Once you login, click on Help for Frequently Asked Questions (FAQs). All
features have descriptions and should be self-explanatory.

For support issues, send email to support@aviatrix.com.

For feedback and feature request, click Make a wish at the bottom of
each page.

Enjoy!

.. |image0| image:: CloudN_Startup_Guide_media/image001.png
   :width: 2.90683in
   :height: 0.35000in
.. |image1| image:: CloudN_Startup_Guide_media/image002.png
   :width: 6.50000in
   :height: 3.65556in
.. |image2| image:: CloudN_Startup_Guide_media/image003.png
   :width: 6.66736in
   :height: 3.75069in
.. |image3| image:: CloudN_Startup_Guide_media/image004.png
   :width: 6.34375in
   :height: 2.49143in
.. |image4| image:: CloudN_Startup_Guide_media/image005.png
   :width: 5.08878in
   :height: 2.24352in
.. |image5| image:: CloudN_Startup_Guide_media/image006.png
   :width: 4.98377in
   :height: 2.19722in
.. |image6| image:: CloudN_Startup_Guide_media/image007.png
   :width: 6.78264in
   :height: 3.42942in
.. |image7| image:: CloudN_Startup_Guide_media/image008.png
   :width: 5.43403in
   :height: 3.40694in
.. |image8| image:: CloudN_Startup_Guide_media/image009.png
   :width: 5.08365in
   :height: 3.25278in
.. |image9| image:: CloudN_Startup_Guide_media/image010.png
   :width: 5.02847in
   :height: 2.76966in
.. |image10| image:: CloudN_Startup_Guide_media/image011.png
   :width: 4.65347in
   :height: 3.86107in
.. |image11| image:: CloudN_Startup_Guide_media/image010.png
   :width: 5.52847in
   :height: 3.04506in
.. |image12| image:: CloudN_Startup_Guide_media/image012.png
   :width: 5.90347in
   :height: 3.25161in
.. |image13| image:: CloudN_Startup_Guide_media/image013.png
   :width: 5.55366in
   :height: 3.60000in
.. |image14| image:: CloudN_Startup_Guide_media/image014.png
   :width: 4.65196in
   :height: 5.04306in
.. |image15| image:: CloudN_Startup_Guide_media/image015.png
   :width: 4.31116in
   :height: 5.29931in
.. |image16| image:: CloudN_Startup_Guide_media/image016.png
   :width: 4.80625in
   :height: 2.45417in
.. |image17| image:: CloudN_Startup_Guide_media/image017.png
   :width: 4.65347in
   :height: 3.51297in
.. |image18| image:: CloudN_Startup_Guide_media/image018.png
   :width: 4.79795in
   :height: 3.60000in
.. |image19| image:: CloudN_Startup_Guide_media/image019.png
   :width: 5.01754in
   :height: 2.42407in
.. |image20| image:: CloudN_Startup_Guide_media/image020.png
   :width: 5.02847in
   :height: 3.94766in
.. |image21| image:: CloudN_Startup_Guide_media/image021.png
   :width: 5.02847in
   :height: 4.76850in
.. |image22| image:: CloudN_Startup_Guide_media/image022.png
   :width: 5.44632in
   :height: 4.97500in
.. |image23| image:: CloudN_Startup_Guide_media/image023.png
   :width: 5.49339in
   :height: 4.97500in
.. |image24| image:: CloudN_Startup_Guide_media/image024.png
   :width: 5.36000in
   :height: 3.35000in
.. |image25| image:: CloudN_Startup_Guide_media/image025.png
   :width: 5.87531in
   :height: 4.20185in
.. |image26| image:: CloudN_Startup_Guide_media/image026.png
   :width: 5.57477in
   :height: 3.97500in
.. |image27| image:: CloudN_Startup_Guide_media/image027.png
   :width: 5.15273in
   :height: 3.67407in
.. |image28| image:: CloudN_Startup_Guide_media/image028.png
   :width: 5.02847in
   :height: 3.60535in
.. |image29| image:: CloudN_Startup_Guide_media/image029.png
   :width: 5.27781in
   :height: 3.53518in
.. |image30| image:: CloudN_Startup_Guide_media/image030.png
   :width: 5.15347in
   :height: 2.87345in
.. |image31| image:: CloudN_Startup_Guide_media/image031.png
   :width: 5.15347in
   :height: 3.63154in
.. |image32| image:: CloudN_Startup_Guide_media/image032.png
   :width: 5.35637in
   :height: 5.10000in
.. |image33| image:: CloudN_Startup_Guide_media/image033.png
   :width: 5.27298in
   :height: 2.85000in
.. |image34| image:: CloudN_Startup_Guide_media/image034.png
   :width: 5.15347in
   :height: 4.24250in
.. |image35| image:: CloudN_Startup_Guide_media/image035.png
   :width: 5.15347in
   :height: 4.24250in
.. |image36| image:: CloudN_Startup_Guide_media/image036.png
   :width: 5.40347in
   :height: 2.92053in
.. |image37| image:: CloudN_Startup_Guide_media/image037.png
   :width: 5.74346in
   :height: 3.10000in
.. |image38| image:: CloudN_Startup_Guide_media/image038.png
   :width: 5.78376in
   :height: 4.03518in
.. |image39| image:: CloudN_Startup_Guide_media/image039.png
   :width: 5.83527in
   :height: 4.10000in
.. |image40| image:: CloudN_Startup_Guide_media/image040.png
   :width: 5.90347in
   :height: 3.76788in
.. |image41| image:: CloudN_Startup_Guide_media/image041.png
   :width: 6.50000in
   :height: 3.82639in
.. |image42| image:: CloudN_Startup_Guide_media/image042.png
   :width: 6.50000in
   :height: 3.54931in
.. |image43| image:: CloudN_Startup_Guide_media/image043.png
   :width: 5.65347in
   :height: 3.50335in
.. |image44| image:: CloudN_Startup_Guide_media/image044.png
   :width: 5.65347in
   :height: 3.53435in
.. |image45| image:: CloudN_Startup_Guide_media/image045.png
   :width: 5.65347in
   :height: 2.18844in
.. |image46| image:: CloudN_Startup_Guide_media/image046.png
   :width: 5.30625in
   :height: 2.97910in
