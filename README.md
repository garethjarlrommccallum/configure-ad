<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Preparing Active Directory Infrastructure in Azure</h1>


<h2>Objective</h2>

- <b>Create two virtual machines (VMs)</b>
- One running Windows Server to act as the Domain Controller.</b>
- Another running Windows 10 to act as a client joining the domain.</b>
  - <b> Deploy Active Directory (AD) in future projects.</b>
- <b>Run a script to create users in the domain.</b>
- <b>Log into the domain from the client VM.</b>
- <b>Manage user accounts and update group policies.</b>
- <b>Simulate a real-life IT environment.!  <br/>
<br />


<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>


<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walk-through:</h2>

<p align="center">
Navigate to Microsoft Azure and create a resource group: <br/>
  
  ![Screenshot 2025-03-13 175344](https://github.com/user-attachments/assets/1f986030-7a40-4686-be35-19fa870c56ba)
<br />
<br />
Setup a virtual network: <br/>

![Screenshot 2025-03-13 180007](https://github.com/user-attachments/assets/db2acff8-2151-4882-b13f-b663b5ee5fc0)
<br />
<br />
- Create and configure a virtual machine using Windows Server. <br />
- Assign the VM to the newly created virtual network in the Networking tab.
- Keep all other settings default and create the VM.

![Screenshot 2025-03-13 182149](https://github.com/user-attachments/assets/e6235f76-50ed-4dd2-a5da-d8b91909ecf5)

![Screenshot 2025-03-13 230059](https://github.com/user-attachments/assets/96c57f65-d6a2-40d1-a9c4-a7c3a6a9e330)
<br />
<br />
Create another virtual machine (VM) to function as the client using a Windows 10:  <br/>

![Screenshot 2025-03-13 190511](https://github.com/user-attachments/assets/9a47f7d0-4b5a-4ca1-8974-32e0f730fb69)

<br />
To ensure our Domain Controller (DC) serves as a reliable DNS server, I’ll switch its private IP allocation from dynamic to static in the network settings. This prevents IP address changes that could disrupt the DNS configuration for the client. <br/>


![Screenshot 2025-03-13 230240](https://github.com/user-attachments/assets/b26baa76-68c2-4a5f-b9c7-297353f4e0c8)

<br />
<br />
I'll connect to the Domain Controller (DC) via Remote Desktop Connection using its public IP and the login credentials set during its creation.
<br />
<br />

![image](https://github.com/user-attachments/assets/de623fd2-3baa-4d8d-909b-68e779dbd833)
<br />
<br />
I'll disable the firewall by right-clicking "Start," selecting "Run," and typing "wf.msc." While not advisable in real-world scenarios, this is fine for the lab.


<img src="https://i.imgur.com/0ztwOZI.png" height="80%" width="80%" alt="Setting Up in Azure"/>

<br />
<br />
Click on "Windows Defender Firewall Properties" then on the, "Domain Profile", "Private Profile, and the "Public Profile" tabs, turn the firewall state off:  <br/>
<img src="https://i.imgur.com/5luuIqk.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/uZJpkGP.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
<img src="https://i.imgur.com/3wiNDiy.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
You should see that all the firewall settings are disable:  <br/>
<img src="https://i.imgur.com/wnHbVDn.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Next, I need configure our clients DNS settings to the DC. To start, back in Azure, I'll grab the DCs private IP address:  <br/>
<img src="https://i.imgur.com/OIzMsfO.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Then, I'll go to the network setting of the client machine. click on the NIC (Network Interface Card), go to settings, then DNS servers and switch from "Inherit from virtual network" to "Custom". Input the DCs private IP here and save:  <br/>
<img src="https://i.imgur.com/ddrkcIQ.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
After that's saved, I'll restart the client machine:  <br/>
<img src="https://i.imgur.com/2C3Qi1q.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Once the machine as restarted, I'll use Remote Desktop connection to connect to the client machine using its public IP and the log in credentials I created while setting up this machine:  <br/>
<img src="https://i.imgur.com/ZgpSqPf.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
Now that I'm logged in, I will open Powershell and attempt to ping the DC using the ping command and its private IP address. In my case it'll look like this. (If there is an error and the connection timed out, double check in Azure to make sure both of the machines are on the same virtual network. If they aren't this is likely causing the error and you'll need to set up the machine again on the same network):  <br/>
<img src="https://i.imgur.com/5bEWedc.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />
While I'm here I can double check that the DNS server settings are pointing to the DC. I'll run "ipconfig /all" and look for the "DNS Servers" and it should point to our DC if everything is set up properly:  <br/>
<img src="https://i.imgur.com/dgShrBB.png" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />
<br />

<h2>Active Directory Infrastructure is Now Prepared! </h2>

<b>We've successfully created two VMs (Virtual Machines), one running Windows Server, to act as a Domain Controller. The other VM as a client, running Windows 10. Don't forget: In later projects I will deploy AD, run a script that will create users in the domain, which I can log into from the client VM, then manage the accounts and update the group policies, all to simulate a real life environment!  </b>
<br />
<br />
</p>

