<p align="center">
<img src="https://i.imgur.com/wrywaeX.png" alt="img"/>
</p>

<h1>Configuration of DNS and CNAME records within Azure Virtual Machines</h1>
This lab builds up on the previous lab (https://github.com/CollinsU99/configure-ad.git), and provides hands-on experience with configuring DNS records and CNAME records to give you a practical understanding of how they work.

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

- Log into Cilent-1 and DC-1 VM via Remote Desktop
- Manually create an A Record in DC-1 called "mainframe"
- In Cilent-1 VM, ping the mainframe A Record
- Run "nslookup mainframe" and "ipconfig /displaydns" in Client-1 VM
- Open DC-1 VM and update mainframe A record to 8.8.8.8
- Open Cilent-1 VM Ping mainframe again
- In Client-1, Run the command "ipconfig /flushdns" as an administartor
- Go back to DC-1 VM and create a CNAME
- Open Cilent-1 VM and Ping CNAME

<h2>Actions and Observations</h2>

<p align="center">
<img src="https://i.imgur.com/QM8c2lU.png" height="80%" width="80%" alt="img"/>
</p>

Let's log into Client-1's VM as jane_admin.

Go to https://portal.azure.com/ and click Virtual machines.

<p align="center">
<img src="https://i.imgur.com/FWvuMXc.png" height="80%" width="80%" alt="img"/>
</p>

Click Client-1

<p align="center">
<img src="https://i.imgur.com/J73jcNu.png" height="80%" width="80%" alt="img"/>
</p>

Copy Client-1 Public Ip address.

<p align="center">
<img src="https://i.imgur.com/nVjRq04.png" height="80%" width="80%" alt="img"/>
</p>

Open Remote Desktop, paste Client-1's public IP address, and click "connect".

<p align="center">
<img src="https://i.imgur.com/Z2qnjQi.png" height="80%" width="80%" alt="img"/>
</p>

Click "More choices" > "Use a different account", type "jane_admin" and "Password1" in the username and password box respectively, and click "Ok". 

<p align="center">
<img src="https://i.imgur.com/p6Qb1ny.png" height="80%" width="80%" alt="img"/>
</p>

Click "Yes", and minimize Client-1's VM.

<p align="center">
<img src="https://i.imgur.com/9kpDOrS.png" height="80%" width="80%" alt="img"/>
</p>

Go back to virtual machines in your Azure portal and click DC-1.

<p align="center">
<img src="https://i.imgur.com/pvSb0tR.png" height="80%" width="80%" alt="img"/>
</p>

Copy DC-1 Public IP address.

<p align="center">
<img src="https://i.imgur.com/9scInGF.png" height="80%" width="80%" alt="img"/>
</p>

Open Remote Desktop, paste DC-1's public IP address, and click "connect".

<p align="center">
<img src="https://i.imgur.com/In69J19.png" height="80%" width="80%" alt="img"/>
</p>

type "jane_admin" and "Password1" in the username and password box respectively, and click "Ok". 

<p align="center">
<img src="https://i.imgur.com/NA9QeOz.png" height="80%" width="80%" alt="img"/>
</p>

Click "Yes".

<p align="center">
<img src="https://i.imgur.com/R0V7sb4.png" height="80%" width="80%" alt="img"/>
</p>

In Client-1, open command prompt and ping mainframe "ping mainframe". 

NOTE: "mainframe" doesn't exist.

Client-1 could not resolve the hostname "mainframe" because it could not find it in its local DNS cache, its local host file, or the DNS server assigned to its NIC.

<p align="center">
<img src="https://i.imgur.com/tYRBMiR.png" height="80%" width="80%" alt="img"/>
</p>

Next, we will create an A record for "mainframe.com".

Go back to DC-1's VM, click the Start Menu, and click "Server Manager".

<p align="center">
<img src="https://i.imgur.com/bjwWAj5.png" height="80%" width="80%" alt="img"/>
</p>

Click the tools tab in the top right corner, and click "DNS".

<p align="center">
<img src="https://i.imgur.com/E5fOdh5.png" height="80%" width="80%" alt="img"/>
</p>

Click "DC-1" and collapse it; collapse "Forward Lookup Zones"; and click "mydomain.com". 

As shown in the image above, you can see the lists of A records (A record maps a host name to an IPv4 address).

You can see that "Client-1" (hostname) maps to 10.0.0.5 (IPv4), and "dc-1" (hostname) maps to 10.0.0.4 (IPv4).

Right-click on an empty space and click "New Host (A or AAAA)..".

<p align="center">
<img src="https://i.imgur.com/3FvdHKA.png" height="80%" width="80%" alt="img"/>
</p>

On the new window, type "mainframe" for the Name box, type DC-1's IP address "10.0.0.4" for the IP address box, and click "Add Host". 

Click "Ok" > "Done".

<p align="center">
<img src="https://i.imgur.com/8xpfpCc.png" height="80%" width="80%" alt="img"/>
</p>

As shown in the image above, "mainframe" is now on our lists of A records, and it maps to DC-1's IP address "10.0.0.4". 

<p align="center">
<img src="https://i.imgur.com/qVLmgKu.png" height="80%" width="80%" alt="img"/>
</p>

In Client-1 VM, ping mainframe by running the command "ping mainframe" on the command prompt.

You can see it actually resolved and pinged DC-1's IP address.

Run "nslookup mainframe" command. You can also see that it returned the record "mainframe.mydomain.com".

<p align="center">
<img src="https://i.imgur.com/DnrbBX1.png" height="80%" width="80%" alt="img"/>
</p>

Run the command "ipconfig /displaydns" to observe the DNS cache of Client-1

The above image shows the DNS cache of "mainframe.mydomain.com", and it's mapped to "10.0.0.4" (A record).

<p align="center">
<img src="https://i.imgur.com/7TCMlos.png" height="80%" width="80%" alt="img"/>
</p>

Go back DC-1 VM, double-click "mainframe", change the IP address to "8.8.8.8", and click "Ok".

<p align="center">
<img src="https://i.imgur.com/6SWmsRO.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Client-1, open command prompt, and run the command "ping mainframe".

Notice that it still resolved the old IP address (10.0.0.4) instead of the new one (8.8.8.8). This is because the record 10.0.0.4 still exists in Clinent-1's local DNS cache

<p align="center">
<img src="https://i.imgur.com/mi8eFR0.png" height="80%" width="80%" alt="img"/>
</p>

Type "cmd" in the search box, click "Run as administrator", and click "Yes" at the prompt.

<p align="center">
<img src="https://i.imgur.com/g1j4L02.png" height="80%" width="80%" alt="img"/>
</p>

Run the "ipconfig /flushdns" command (this will wipe out Client-1's DNS cache, and let's it repopulate by quering the DNS server).

Run the "ipconfig /displaydns" command. There's no DNS to display because they have all been flushed out.

Now, run the command "ping mainframe". You can see it resolved to "8.8.8.8".

<p align="center">
<img src="https://i.imgur.com/EaCPwc2.png" height="80%" width="80%" alt="img"/>
</p>

Next, we will create a CNAME record that matches the name search to "www.google.com".

In DC-1 VM, open the DNS manager, right-click on the empty space, and click "New Alias (CNAME)".

<p align="center">
<img src="https://i.imgur.com/jED5AGM.png" height="80%" width="80%" alt="img"/>
</p>

Let's name it "search, associate it with "www.google.com", and click "Ok".

NOTE: This won't have any utility; it will just show that we can map names to other names.

<p align="center">
<img src="https://i.imgur.com/HZhuo3f.png" height="80%" width="80%" alt="img"/>
</p>

You can see that "search" is now on our list of records.

<p align="center">
<img src="https://i.imgur.com/HEQcWhB.png" height="80%" width="80%" alt="img"/>
</p>

Go back to Client-1 VM, open command prompt as administartor, and run the command "ipconfig /flushdns".

Run "ping search" command. Notice that it resolved to "www.google.com". This is because we forced it to do so through the CNAME record.

Run "ipconfig /displaydns" command and observe that "search.mydomain.com" resolves to the CNAME record "www.google.com", and "www.google.com" resolves to the A record "142.250.68.68".





