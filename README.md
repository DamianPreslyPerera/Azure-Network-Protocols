
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

  
