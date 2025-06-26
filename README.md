<h1>Azure Network Traffic Analysis Lab</h1>

<h2>Description</h2>
<p>This project simulates real-world IT scenarios by creating two virtual machines (Windows and Linux) in Microsoft Azure, then analyzing network traffic using Wireshark. It includes observing common protocols like ICMP, SSH, DNS, DHCP, and RDP.</p>

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure – Cloud platform for creating and managing virtual machines and networks</li>
  <li>Remote Desktop Protocol (RDP) – To connect to the Windows 10 VM</li>
  <li>Wireshark – Network protocol analyzer used for traffic capture</li>
  <li>Windows PowerShell – Used for ping tests and network diagnostics</li>
  <li>Linux (Ubuntu 22.04) – Target machine for ICMP and SSH testing</li>
  <li>Windows 10 – Source machine used to initiate traffic and analysis</li>
  <li>Network Security Groups (NSG) – Azure's firewall-like feature to allow or deny traffic</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows 10 (Client VM)</li>
  <li>Ubuntu Linux 22.04 LTS (Server VM)</li>
</ul>

<h2>High-Level Deployment and Configuration Steps</h2>
<ol>
  <li>Create a Resource Group in Azure</li>
  <li>Deploy a Windows 10 VM and allow it to create a new Virtual Network and Subnet</li>
  <li>Deploy an Ubuntu VM into the same Resource Group and Virtual Network</li>
  <li>Connect to the Windows VM using RDP and install Wireshark</li>
  <li>Analyze ICMP traffic by pinging the Ubuntu VM and public websites</li>
  <li>Modify Network Security Group rules to block and allow ICMP traffic</li>
  <li>Use SSH from Windows to Ubuntu and observe the traffic in Wireshark</li>
  <li>Renew the IP address to observe DHCP traffic</li>
  <li>Use nslookup to generate DNS traffic</li>
  <li>Capture and filter RDP traffic in Wireshark</li>
</ol>

<h2>Deployment and Configuration Steps</h2>

<h3>1. Creating the Virtual Machines in Azure</h3>
<img src="https://i.imgur.com/n6abxU2.png" alt="Creating Windows VM in Azure" width="600"/>
<img src="https://i.imgur.com/0MLWPcN.png" alt="Creating Windows VM in Azure" width="600"/>
<img src="https://i.imgur.com/GkUYoPq.png" alt="Creating Windows VM in Azure" width="600"/>

<p>I created a new Resource Group and deployed a Windows 10 and Ubuntu Virtual Machine. During setup, I allowed Azure to automatically create a new Virtual Network and Subnet.</p>

<h3>2. Adding the Ubuntu VM to the Same Network</h3>
<img src="https://i.imgur.com/SzSmFFm.png" alt="Creating Ubuntu VM in same VNet" width="600"/>
<p>I deployed an Ubuntu VM into the same Resource Group and selected the same Virtual Network created earlier. Both VMs are now in the same subnet.</p>

<h3>3. Connecting to the Windows 10 VM via Remote Desktop</h3>
<img src="https://i.imgur.com/uc8W0zU.png" alt="Remote Desktop Connection to Windows VM" width="600"/>
<p>After both virtual machines were created in Azure, I connected to the Windows 10 VM using <strong>Remote Desktop Connection (RDP)</strong>.</p>
<p>I used the public IP address provided in the Azure portal, along with the username and password set during VM creation. This allowed me to access the Windows desktop environment remotely from my local computer.</p>
<p>Once connected, I was able to begin installing and running tools like Wireshark, PowerShell, and initiate traffic toward the Ubuntu VM for analysis.</p>

<h3>4. Installing and Using Wireshark</h3>
<img src="https://i.imgur.com/tCca6TI.png" alt="Installing Wireshark" width="600"/>
<p>Connected to the Windows VM via RDP and installed Wireshark to capture and analyze network traffic.</p>

<h3>5. Observing ICMP Traffic</h3>
<img src="https://i.imgur.com/nTaSt4t.png" alt="ICMP Ping Ubuntu" width="600"/>
<p>Started a packet capture in Wireshark and filtered by ICMP. I pinged the Ubuntu VM’s private IP from the Windows VM and observed the requests and replies.</p>

<h3>6. Observing Public Ping Traffic</h3>
<img src="https://i.imgur.com/XckY1Ip.png" alt="Public Ping Google" width="600"/>
<p>Used PowerShell to ping www.google.com and observed the ICMP packets to and from the public address in Wireshark.</p>

<h3>7. Configuring Network Security Group (Firewall)</h3>
<img src="https://i.imgur.com/iIjo2l0.png" alt="NSG Blocking ICMP" width="600"/>
<img src="https://i.imgur.com/hrDbT5n.png" alt="NSG Blocking ICMP" width="600"/>
<p>Initiated a continuous ping from Windows to Ubuntu, then modified the Ubuntu VM’s Network Security Group to block inbound ICMP traffic. Observed that the ping failed and no ICMP packets were seen in Wireshark.</p>
<img src="https://i.imgur.com/6LVUzyg.png" alt="NSG Blocking ICMP" width="600"/>

<h3>8. Re-Enabling ICMP Traffic</h3>
<img src="https://i.imgur.com/6jKbIlw.png" alt="NSG Allowing ICMP" width="600"/>
<img src="https://i.imgur.com/Vgdc7G9.png" alt="NSG Allowing ICMP" width="600"/>
<p>Re-enabled ICMP in the NSG. Verified that the ping resumed and ICMP packets were visible again in Wireshark.</p>

<h3>9. Observing SSH Traffic</h3>
<img src="https://i.imgur.com/X7tQr4w.png" alt="SSH Traffic Wireshark" width="600"/>
<p>Filtered Wireshark for SSH traffic. Used PowerShell in Windows to SSH into the Ubuntu VM using its private IP, then executed basic commands to observe encrypted SSH communication.</p>

<h3>10. Observing DHCP Traffic</h3>

<p>Filtered for DHCP in Wireshark. Ran ipconfig /renew in PowerShell to request a new IP address and observed the DHCP request and response traffic.</p>

<h3>11 Observing DNS Traffic</h3>
<img src="https://i.imgur.com/AYosR25.png" alt="DNS Lookup Traffic" width="600"/>
<p>Filtered for DNS traffic. Used nslookup to query domains like google.com and disney.com and confirmed DNS requests and responses in Wireshark.</p>

<h3>12 Observing RDP Traffic</h3>
<img src="https://i.imgur.com/hEOTxCO.png" alt="RDP Wireshark" width="600"/>
<p>Filtered for RDP traffic using tcp.port == 3389. Verified the presence of RDP packets during the remote desktop session to the Windows VM.</p>
