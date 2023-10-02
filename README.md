
![68747470733a2f2f692e696d6775722e636f6d2f55613775646f532e706e67](https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/90bd3487-9022-448d-9852-f88a3760af37)


# Azure Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines
In this demonstration, I observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups

## Environments and Technologies Used
* Microsoft Azure (Virtual Machines/Compute)
* Remote Desktop
* Various Command-Line Tools
* Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
* Wireshark (Protocol Analyzer)

## Operating Systems Used
* Windows 10 (21H2)
* Ubuntu Server 20.04

## High-Level Steps
* Create two Virtual Machines 
* Download Wireshark 
* Inspect Network Traffic
* Experiment with Azure NSG Firewall rules to Deny/Allow network traffic


## Creating two Virtual Machines

Following the same steps as the [Create a Virtual Machine](https://github.com/DamianPreslyPerera/Azure-Virtual-Machine) lab, create another virtual machine that is running a Ubuntu Server Image 

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/b7d9123a-65f6-4ccf-a1d4-fd5a01bb0bfe">

---

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/0a8abb88-d9c2-4f44-9fbf-097f0333c3d6">

* Chose the "VM1-vnet" virtual network, this was already created in the previous lab
* Choose the default subnet
* Click the "Review + Create" button

---
You should now be able to view both Virtual Machines
* One VM is running Windows, and the other Linux

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/353b6807-0919-4ef5-a46f-6e5fe6400356">

---

Click on the newly created VM (VM2) to view its configuration settings
* Take note of  VM's "Private IP Address"
* You will be using this IP address within VM1 to inspect network traffic
  
<img width="1128" alt="Screenshot 2023-10-02 120842vm2IP" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/23ea8ac7-1513-48e3-af76-adbc27bea893">

---

## Installing & Using Wireshark

Navigate to VM1 (The virtual machine running Windows)
* [Download Wireshark](https://www.wireshark.org/download.html)
* Click through the Wireshark installer prompts
* Open Wireshark after installation completes

<img width="373" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/ed85de76-2963-4421-a401-1db8869eb4e9">

---

Your Wireshark Application should look like this

<img width="751" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/7ff832fb-f435-47d5-8ecf-bef227887a51">

--- 
In order to start inspecting network traffic
* Choose the "Ethernet Adapter"
* Click on the Blue icon to start analyzer

You will be able to view the network traffic occuring on the virtual machine

<img width="752" alt="Screenshot 2023-10-02 135205wirshiperased" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/89a19cbb-f0cc-4953-a9b4-0a722704d3e5">

















