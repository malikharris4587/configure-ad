<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

Watch for an easy tutorial! In the video i go a step further and use Powershell ISE to create user accounts and log into the client with a newly generated account. 
- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute][(https://www.youtube.com)](https://youtu.be/ziH9YsW2PrY)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Use Azure and create a Windows server virtual machine 
- Create a client virtual machine on the same virtual network as the Windows server
- Install Active Directory on the server VM
- Promote it to a domain controller

<h2>Deployment and Configuration Steps</h2>
First, log in to the Azure portal and create a virtual machine. This virtual machine will be configured as a Windows server. You can call it DC-1 since this will become our Domain Controller. A domain controller is simply a server with Active Directory installed on it. Select the size with 2 vcpus as shown in the picture.
</p>
<br />

<img width="565" alt="Screen Shot 2023-08-29 at 9 07 09 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/693e485d-2465-4c7e-a096-76a0292b6406">
<img width="538" alt="Screen Shot 2023-08-29 at 9 10 16 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/5462fd19-1169-4cd3-9d92-2db5416d34a2">
<p>

<p>
Next, wait a few minutes then create a Windows virtual machine with Windows 10. Wait a few minutes after the deployment finishes because if you don't configure the network for the Windows client virtual machine, it may not populate the virtual network that was generated after you created the server. You need this network to populate so you can add it to your Windows client. Otherwise, the only option you will see will be Azure creating a new network. You don't want that. To help, go to the server virtual machine and you can see what the network is. It may be different for everyone. After you complete this. log into both virtual machines (using Microsoft Remote desktop on mac/Remote desktop on windows) and use the command prompt to ping the private ip address of the Winows server. It will fail because the firewall is closed. To open a hole in the firewall, Log into the windows server using the public ip address. In the search bar type in firewall and look for windows firewall advanced security. Make it full screen>click on inbound rules to the left>slide to the right and click protocol>locate ICMPv4 and enable the first two ICMPv4 echo requests. THis opens the firewall. Retry pinging the Server from the Client and you will start seeing traffic in the command prompt on the client. 
</p>
<br />

<img width="553" alt="Screen Shot 2023-08-29 at 9 10 09 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/a4176258-082e-4a97-bf22-43dc3294e67e">
<img width="568" alt="Screen Shot 2023-08-29 at 9 13 45 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/17a97c10-9b67-4371-acf1-a940321e0268">
<img width="595" alt="Screen Shot 2023-08-29 at 9 19 25 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/b625eb4a-b9cb-48c5-b099-47d1d4183faa">
<img width="687" alt="Screen Shot 2023-08-29 at 9 21 00 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/4b080e50-ddf3-43b9-8d05-686b5f451ef9">
<img width="553" alt="Screen Shot 2023-08-29 at 9 22 13 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/a8632980-84df-445c-a811-a28f77131299">
<img width="1338" alt="Screen Shot 2023-08-29 at 9 24 04 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/aa4fa48c-c7f7-44fb-8fd1-d92b9929eac7">
<img width="687" alt="Screen Shot 2023-08-29 at 9 25 07 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/6feda5f5-f35b-4a29-8586-4a64885708f9">


On the Windows server a Server manager window should have popped up when you first logged in. Click "add roles". Click next until you get to the second picture above. Click on domain Services. then keep clicking thorugh and install. After thats done, click on the flag/caution sign on the top right of the screen. Then click on the blue link that says to promote the server to a domain controller. Then click on add a new forest>type in your organizations name (for this example its a generic domain as seen in the photo)>after thats complete and you install, your virtual machine will restart. Log back in. You now have acitve directory installed on your server. You can create, admins and orgainzational units if you want here. This is pretty much synonymous with creating student profiles on a server for a college campus. 
</p>
<br />

<img width="1336" alt="Screen Shot 2023-08-29 at 9 26 38 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/4a8f2262-aa4e-4e8e-8bee-e0eb6361e096">
<img width="550" alt="Screen Shot 2023-08-29 at 9 27 33 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/24f0c947-a053-44f4-9e79-60aa144bcace">
<img width="1336" alt="Screen Shot 2023-08-29 at 9 29 50 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/0eb24629-1dba-46d9-b6a9-c0d0f54bafbd">
<img width="533" alt="Screen Shot 2023-08-29 at 9 32 28 AM" src="https://github.com/malikharris4587/configure-ad/assets/143438495/437b61d9-565f-4534-ac1f-d96241877053">

<p>

