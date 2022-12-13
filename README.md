<p align="center">
<img src="https://i.imgur.com/9TGxHYd.jpg" alt="Domain Name System Logo"/>
</p>

<h1>Configuring DNS settings within Azure</h1>
This tutorial outlines the implementation of DNS settings within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- A-Record Exercise
- Local DNS Cache Exercise
- CNAME Record Exercise

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/q9xVERK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This is a continuation of the Active Directory project. Ping "mainframe" on Client-1 and notice it can't resolve.
</p>
<br />

<p>
<img src="https://i.imgur.com/Z29QJDu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Let's create mainframe.mydomain.com. Click Start and open Server Manager on DC-1 if it's not open.
</p>
<br />

<p>
<img src="https://i.imgur.com/1akiTG5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on tools on the upper right and then DNS.
</p>
<br />

<p>
<img src="https://i.imgur.com/nlWZQ7O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on DC-1 then Foward Lookup Zones and then mydomain.com.
</p>
<br />

<p>
<img src="https://i.imgur.com/2EpJOu6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click and click on new host.
</p>
<br />

<p>
<img src="https://i.imgur.com/EKAfjWT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a new IP Address. I used the same one as DC-1, "10.0.0.4".
</p>
<br />

<p>
<img src="https://i.imgur.com/cxVUgF5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click add host and observe that mainframe is now created.
</p>
<br />

<p>
<img src="https://i.imgur.com/HOtmuQa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ping Mainframe again on Client-1 and notice it pings.
</p>
<br />

<p>
<img src="https://i.imgur.com/3fPEsvP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type "nslookup mainframe" and notice that DC-1 returned the record mainframe.mydomain.com.
</p>
<br />

<p>
<img src="https://i.imgur.com/mULajEd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type "ipconfig /displaydns" and notice that mainframe.mydomain.com is mapped to 10.0.0.4
</p>
<br />

<p>
<img src="https://i.imgur.com/MCBPUxV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 and update mainframe IP Address to 8.8.8.8 then click apply.
</p>
<br />

<p>
<img src="https://i.imgur.com/CdNf1bi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
"mainframe" now has an IP address of 8.8.8.8.
</p>
<br />

<p>
<img src="https://i.imgur.com/6H20M8z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 and ping mainframe again. Notice it still pings 10.0.0.4 Even though the IP address was changed it pings the old address because of the DNS cache.
</p>
<br />

<p>
<img src="https://i.imgur.com/mBryCRk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use ipconfig /displaydns and notice that the IP address is the old one for mainframe.
</p>
<br />

<p>
<img src="https://i.imgur.com/538A8OT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type ipconfig /flushdns. If elevation is required, open command prompt as administrator by right clicking.
</p>
<br />

<p>
<img src="https://i.imgur.com/wQ4Axr8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Try ipconfig /flushdns again and notice that DNS gets flushed
</p>
<br />

<p>
<img src="https://i.imgur.com/UL980vz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ping mainframe and observe that the new IP address has been retrieved from the record.
</p>
<br />

<p>
<img src="https://i.imgur.com/u16jg8z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Type ipconfig /displaydns and notice that 8.8.8.8 is now cached.
</p>
<br />

<p>
<img src="https://i.imgur.com/QXH5lQH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now ping "search" and observe what happens.
</p>
<br />

<p>
<img src="https://i.imgur.com/iLijhxP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DNS Manager on DC-1 and create a new CNAME record.
</p>
<br />

<p>
<img src="https://i.imgur.com/zMyWkhT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a search record and associate it with www.google.com. This is how you map names to other names.
</p>
<br />

<p>
<img src="https://i.imgur.com/V9ejQAE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
"search" is now mapped to www.google.com.
</p>
<br />

<p>
<img src="https://i.imgur.com/9wkkwMM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to Client-1 and ping search and notice it now pings www.google.com.
</p>
<br />
