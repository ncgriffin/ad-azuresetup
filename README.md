<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

<p>This a detailed tutorial for deploying an on-premises Active Directory within Azure Virtual Machines. It involves setting up and configuring a Domain Controller (DC-1) and a client machine (Client-1), both using Microsoft Azure, Active Directory Domain Services, and PowerShell. The guide includes steps for creating and configuring virtual machines, setting static IP addresses, ensuring network connectivity, and enabling ICMP traffic for communication between the machines. This setup serves as a foundation for more advanced configurations in Azure and Active Directory.</p>


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

- Create a virtual machine on Azure
- Name it DC-1 
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="730" alt="VM image" src="https://imgur.com/03AsXRe.png">

</p>
<p>


<strong> NOTE: Select at least 2 vcpus and 16 GiB memory and take note of the Virtual Network (vnet) that the VM has created.</strong>
</p>
<br />

<p>
<img width="820" alt="DC-vm" src="https://imgur.com/lHv5uAG.png">
</p>
<p>
</p>
<br />


<h3>&#9313; Set the Domain Controller's Private IP Address to Static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking"
<img width="400" alt="networking" src="https://imgur.com/VWQVmHK.png">
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to Static

<br>

<p>
<img width="475" alt="static" src="https://imgur.com/PY3l6pW.png">
</p>

<br />


<h3>&#9314; Create the client VM </h3>

- Create a new VM and this time name it Client-1. Select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="700" alt="VM 2 name " src="https://imgur.com/pYF0M2M.png">

<br>
<br>

<p><strong> NOTE: Select the same resource group and vnet from the DC-1 VM </strong></p>


<img width="820" alt="VM2 vnet" src="https://imgur.com/ckSNrVP.png">\


Finalize and wait for the VM's deployment


<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the Domain Controller from the Client.</p>

- Login to Client-1 using it's Public IP Address on Remote Desktop

<img width="750" alt="client 1 public ip" src="https://imgur.com/LEvHeEc.png">




<p><strong> Locate DC-1's Private IP Address in the Azure portal and copy it. Proceed to Client-1 and open the Command Prompt, type "ping -t (DC-1 Private IP Address)" </strong></p>


<img width="720" alt="perpetual ping" src="https://imgur.com/cM7jL9C.png">


<br>
<br>

<p> <strong> Notice how the request continues to time out, this is due in part because ICMPv4 traffic is blocked by default on DC-1's firewall. Therefore, we will have to enable inbound ICMP traffic to allow for Client-1's continuous ping to be successful.</strong> </p>


<p><strong> Login to DC-1 using Remote Desktop -> open Windows Defender Firewall -> Select Advanced Settings -> Sort by Protocol (ICMPv4) -> Enable these specfic rules by using right click</strong></p>

<br>

<img width="800" alt="firewall" src="https://imgur.com/253uwfO.png">

<br>

<img width="800" src="https://imgur.com/DuKwtPP.png">


<p><strong> Once the traffic has been enabled, you can look at Client-1 and see the continuous ping is now successful.</strong> </p>

<img width="650" alt="ping 2" src="https://imgur.com/MdciPsh.png">

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>









