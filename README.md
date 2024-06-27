<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>


<p>This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.
</p>

<h2>Overview </h2>

<p>In this initial project, I will set up and link two virtual machines, each with a specific function. The first virtual machine will serve as the Domain Controller (DC-1), while the second will be configured as the Client (Client-1).</p>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>High-Level Deployment Configuration Steps</h2>

<h3>&#9312; Create the Domain Controller</h3>

- Create a virtual machine on Azure.
- Name it DC-01 
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="730" alt="VM image" src="https://imgur.com/03AsXRe.png">

</p>
<p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<strong> NOTE: Make sure to select at least 2 vcpus and 16 GiB memory and take note of the vnet that the VM has created.</strong>
</p>
<br />

<p>
<img width="820" alt="DC-vm" src="https://imgur.com/lHv5uAG.png">
</p>
<p>
</p>
<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>


<h3>&#9313; Set the Domain Controller's Private IP to static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking" on the left side. 
<img width="400" alt="networking" src="https://imgur.com/VWQVmHK.png">
<br>
<br>
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to static.

<br>

<p>
<img width="475" alt="static" src="https://imgur.com/PY3l6pW.png">
</p>

<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>


<h3>&#9314; Create the client VM </h3>

- Once again create a new VM and we'll name it Client-01. We'll select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="700" alt="VM 2 name " src="https://imgur.com/pYF0M2M.png">

<br>
<br>

<p><strong> NOTE: Make sure to select the same resource group and vnet from the DC-01 VM </strong></p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="820" alt="VM2 vnet" src="https://imgur.com/ckSNrVP.png">\

<p><strong>.</strong></p>
<p><strong>.</strong></p>

Now finalize everything and wait for its deployment.

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the domain controller from the client.</p>

- First login to the Client-01 using it's public ip address and remote desktop

<img width="750" alt="client 1 public ip" src="https://imgur.com/LEvHeEc.png">


<p><strong>.</strong></p>
<p><strong>.</strong></p>


<p><strong> Find DC-01's private ip address in the Azure Portal and copy it. Proceed to Client-01 and open the terminal and type "ping -t (DC-01 private ip address)" </strong></p>


<img width="720" alt="perpetual ping" src="https://imgur.com/cM7jL9C.png">


<br>
<br>

<p> <strong> Now notice how the request timed out, this is because ICMP v4 traffic is blocked by default on DC-01's firewall. So we will have to enable inbound ICMP traffic to allow for Client-01's ping.</strong> </p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Login to DC-01 using remote desktop and open windows defender firewall and select advanced settings. Sort by protocol and find both ICMP echo requests and enable both these rules by right clicking and selecting enable rule.</strong></p>

<br>

<img width="800" alt="firewall" src="https://imgur.com/253uwfO.png">

<br>

<img width="800" src="https://imgur.com/DuKwtPP.png">

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now once the traffic has been enabled, you can check back with Client-01 and notice that the ping is now successful.</strong> </p>

<img width="650" alt="ping 2" src="https://imgur.com/MdciPsh.png">

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>









