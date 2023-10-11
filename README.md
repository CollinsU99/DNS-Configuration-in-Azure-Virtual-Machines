<p align="center">
<img src="https://i.imgur.com/wrywaeX.png" alt="img"/>
</p>

<h1>Configuration of DNS and CNAME records within Azure Virtual Machines</h1>
This tutorial builds up on the previous lab (https://github.com/CollinsU99/configure-ad.git). It provides hands-on experience with configuring DNS records and CNAME records to give you a practical understanding of how they work.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Active Directory Domain Services
- Server Manager
- DNS Manager
- Command Prompt (Admin)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)

<h2>High-Level Steps</h2>

- Log into Cilent-1 and DC-1 VM 
- Go to DC-1 VM/ DNS Manager/ Forward Lookup Zones / Create A Record
- Open Cilent-1 VM ping A Record from DC-1
- Flush DNS and Display DNS on Cilent-1
- Open DC-1 VM and change the name of the A Record
- Open Cilent-1 VM Ping the new name of A Record
- Go back to DC-1 VM and create a CNAME
- Open Cilent-1 VM and Ping CNAME
- Go back to DC-1 VM and see Root Hints File


<h2>Actions and Observations</h2>
