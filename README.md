<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>


<p>
Inside Azure portal type: “virtual machine” in search bar and click on virtual machine. Then click “+ Create” on the top left. 
*note: this configuration of VM is special for the following lab, you can configure the VM as you need
</p>
<p>
<img src="https://i.imgur.com/JpSxAdj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
First, select the subscription you have, then create a new Resource group and call it AD-lab, then name the VM DC-1 (DC stand for Domain Control), pick a Region that is closest to you. Choose “Windows Server 2022 Datacenter: Azure – Gen 2” for the image, and for the size pick “Standard_E2s_V3 – 2vcpus”. Then pick a name and user name (DO NOT FORGET THESE!). Finally, under Licensing, click both squares. 
To create the VM click on “Create” at the bottom of the page 
</p>
<p>
<img src="https://i.imgur.com/9TXUB68.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Create a second VM named “Client-1” using the same Resource group, Region, Size of VM. For image select Windows 10.
Click Next twice until you reach the Networking configuration, in there make sure that this VM is in the same Virtual Network than the previous VM (DC-1). Then click on Review + Create
</p>
<p>
<img src="https://i.imgur.com/KUiCAWI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
We need to change the IP address of DC-1 from dynamic to static.
Go to Virtual Machine, click on DC-1, got to Networking, and on the top you will find “Network Interface: xx-xxxx” Click on it. Once inside, click IP configuration on the left bar, then click in “ipconfig1” at the bottom of the page. Next, under “Assigment” change it from “Dynamic” to “Static”.
</p>
<p>
<img src="https://i.imgur.com/K5oXPfu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Now let’s make sure there is connectivity between the client and Domain Controller.
On DC-1, 
To log in DC-1, first go to VM page in Azure, then click on DC-1, inside you will see “Public IP address”, copy that Ip, then if you are in Windows, click on the search bar in your Taskbar, and type: “Remote Desktop Connection”, Once inside, paste the IP address, and type the user name and password you gave it when creating the VM. 
</p>
<p>
<img src="https://i.imgur.com/sPvcdBp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Once inside DC-1, at the taskbar on desktop type: “wf.msc” , click on Inbound Rules at the left bar, then sort by protocol, click the options with “ICMPv4” as their protocol and click enable. 
</p>
<p>
<img src="https://i.imgur.com/XZjJHcF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Now using the same steps as before, log in Client one. At the search bar type “cmd” In the command line type: “ping -t x.x.x.x”, where x.x.x.x is the private IP address of DC-1, which can be found in its portal page in Azure.  If you get something like “Reply from 10.2.0.4: bytes=32 time=11ms TTL=118” Then there is a connection between Client-1 and DC-1. If you see an error that says “Request time out” you probably didn’t enable correctly the ICMPv4 protocol inside DC-1. 
</p>
<p>
<img src="https://i.imgur.com/YLnUMRo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />




