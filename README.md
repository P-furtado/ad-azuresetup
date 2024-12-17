<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Building the Foundation: Preliminary Setup for Active Directory and Network Traffic Analysis between Azure VMs</h1>


<p>Welcome to the inaugural project in a comprehensive series of tutorials focused on Azure and Active Directory implementation. This initial project serves as the foundational cornerstone and setup for the subsequent  parts of this tutorial series. The primary objective is to lay the groundwork for a simple lab environment on Azure to simulate the environment in which Active Directory is employed within an enterprise setting.
</p>

<h2>Overview </h2>

<p>In this first project, I will configure and interconnect two virtual machines, each assuming distinct roles. The first virtual machine will be designated as the Domain Controller. The second virtual machine will be configured as the Client.</p>

<h2>Key Objectives</h2>
<h3>Virtual Machine Setup</h3>

-  Configure the Domain Controller virtual machine
-  Establish the Client virtual machine

<h3>Remote Connectivity</h3>

- Enable a connection using remote desktop connection

<h3> Traffic Inspection</h3>

- Undertake a basic inspection of the network traffic between the Domain Controller and Client virtual machines.



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Create the Domain Controller</h3>

- Create a virtual machine on Azure.
- Name it DC-01 
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="776" alt="VM image" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303159359-f072cd7b-b547-4006-9ddb-ae6ba39c497e.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145136Z&X-Amz-Expires=300&X-Amz-Signature=b52ab8c2f257a71f965bd1123c12653a53a8d52ff9e1a933ac355d3bff06933c&X-Amz-SignedHeaders=host">
</p>
<p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<strong> NOTE: Make sure to select at least 2 vcpus and 16 GiB memory and take note of the vnet that the VM has created.</strong>
</p>
<br />

<p>
<img width="736" alt="DC-vm" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303161586-323e78b9-4e86-46e3-b021-6ac529ccb600.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T150141Z&X-Amz-Expires=300&X-Amz-Signature=e437ce75ec21b7968479adb0f3997ee4e2d05c4b95f45a679e3defbd6623c339&X-Amz-SignedHeaders=host">
</p>
<p>
</p>
<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Set the Domain Controller's Private IP to static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking" on the left side. 
<img width="692" alt="networking" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303160797-a35e1aad-57e1-4c1c-9e4e-aefa4fcf31ea.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145555Z&X-Amz-Expires=300&X-Amz-Signature=7e5f06debe5857c453a5d0696d1ae1306797af8260a7c59df9477bf3ec2b7b42&X-Amz-SignedHeaders=host">
<br>
<br>
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to static.

<br>

<p>
<img width="518" alt="static" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303162291-8629a747-9809-4329-859f-2d38896ec484.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145622Z&X-Amz-Expires=300&X-Amz-Signature=13037afd45c3587a1586936a7fc0c2eda5fc3685d0f68b3913e692fd73472034&X-Amz-SignedHeaders=host">
</p>

<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Create the client VM </h3>

- Once again create a new VM and we'll name it Client-01. We'll select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="717" alt="VM 2 name " src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303169519-a3005b2a-cc0a-49f6-8b9e-c6a594c2aba9.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145742Z&X-Amz-Expires=300&X-Amz-Signature=fca8cd046601f00d3c039628697396c28251afcd65f87cd03ec36997957b89ec&X-Amz-SignedHeaders=host">

<br>
<br>
<br>

<p><strong> NOTE: Make sure to select the same resource group and vnet from the DC-01 VM </strong></p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="731" alt="VM2 vnet" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303169677-d591d9b0-ce68-4e74-a466-cdd34886c74b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145758Z&X-Amz-Expires=300&X-Amz-Signature=a542c5c290339e6f292bcf0a9cce902b197eb147f7749399d5ad4b8a815da379&X-Amz-SignedHeaders=host">\

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

- Now finalize everything and wait for its deployment.

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the domain controller from the client.</p>

- First login to the Client-01 using it's public ip address and remote desktop

<img width="993" alt="client 1 public ip" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303171349-c12a5300-fd26-4ae7-b15b-b4fee053bece.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145818Z&X-Amz-Expires=300&X-Amz-Signature=a7083e659bb73480b86665568e27a4f49bf85d3f2bf098e421b2126254de22e3&X-Amz-SignedHeaders=host">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="297" alt="remote desktop first login" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303171051-97467245-a6b9-4922-a668-71fdf6f77989.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145837Z&X-Amz-Expires=300&X-Amz-Signature=74187ad9f4d24c8c7cf960bf1bdaf3877f976911cb1c2ea0270796a7239e4038&X-Amz-SignedHeaders=host">

<br>
<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Find DC-01's private ip address in the Azure Portal and copy it. Proceed to Client-01 and open the terminal and type "ping -t (DC-01 private ip address)" </strong></p>


<img width="668" alt="perpetual ping" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303172153-d83a1cbf-2619-4382-bc3c-7025ed246119.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T145854Z&X-Amz-Expires=300&X-Amz-Signature=6ad4dc6d2410728ec45940ae3ac14e3d7c8dd0fa5f037aa3b618fad2cb0aeb9e&X-Amz-SignedHeaders=host">


<br>
<br>

<p> <strong> Now notice how the request timed out, this is because ICMP v4 traffic is blocked by default on DC-01's firewall. So we will have to enable inbound ICMP traffic to allow for Client-01's ping.</strong> </p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Login to DC-01 using remote desktop and open windows defender firewall and select advanced settings. Sort by protocol and find both ICMP echo requests and enable both these rules by right clicking and selecting enable rule.</strong></p>

<br>

<img width="668" alt="firewall" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303172920-818f7ebe-2ec3-4bd5-b59a-2bc55c24a567.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T150000Z&X-Amz-Expires=300&X-Amz-Signature=557ddbfe6dffb783cccc8abe5d77a91b95e9de24a47a517d035e983deab55e5f&X-Amz-SignedHeaders=host">

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now once the traffic has been enabled, you can check back with Client-01 and notice that the ping is now successful.</strong> </p>

<img width="334" alt="ping 2" src="https://github-production-user-asset-6210df.s3.amazonaws.com/158519921/303174738-ede5ce46-2d9d-49c6-82d7-5afc9796294b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241217%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241217T150018Z&X-Amz-Expires=300&X-Amz-Signature=e23f56bb179877d3e4448dfe4ae67837e54349862341c870632faedf0e91d0db&X-Amz-SignedHeaders=host">

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>
