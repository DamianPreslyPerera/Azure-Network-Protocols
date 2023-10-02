
![68747470733a2f2f692e696d6775722e636f6d2f55613775646f532e706e67](https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/90bd3487-9022-448d-9852-f88a3760af37)


# Azure Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines

This project involves a hands-on exploration of network traffic within Microsoft Azure Virtual Machines. Utilizing tools like Wireshark and experimenting with Network Security Groups, this demonstration includes the observation of various network protocols such as SSH, RDP, DNS, HTTP/S, and ICMP. The project encompasses the creation of virtual machines, the installation of Wireshark, monitoring network traffic, testing connectivity between VMs, and fine-tuning Azure NSG Firewall rules to manage and control network traffic effectively.

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
* Ping VMs across network
* Experiment with Azure NSG Firewall rules to Deny/Allow network traffic
* Use SSH protocol to access Linux VM through Windows


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

---

## Ping VMs Across Network

* Now that you have set up both VMs and have Wireshark running on one VM1, we can proceed to send traffic to VM2
* We can accomplish this by using Windows Powershell on VM1 and using the "ping" command to contact VM2

### Powershell
* Open Powershell on VM1
* Type in the following command: ping 10.0.0.5
* 10.0.0.5 is the IP Address of VM2

<img width="613" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/1b3d1433-9614-4cfb-963e-a6eceec09289">

The image shows that VM1 is able to succesfully ping VM2 and send packets to it across the network

---
### View ICMP traffic with Wireshark

* Open Wireshark and type in "icmp" on the filter bar
* Start capturing packets
* Ping VM2 again using the ping command

<img width="1065" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/9702804d-528f-47ae-abb7-e53e6690abcf">

You can now view the network traffic of VM1 communicating with VM2
* The IP Address of VM1 is 10.0.0.4
* The IP Address of VM2 is 10.0.0.5
* The VMs use ICMP (Internet Control Message Protocol) to communicate across the network


## Experiment with Azure NSG Firewall rules to Deny/Allow network traffic

Go back to the Azure Portal and click on the "Network Security Groups" icon

<img width="1128" alt="Screenshot 2023-10-02 141353secgroup" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/ba3e3dbd-255c-4a08-a5dc-46fac32abaf8">

---

Click on "VM2-nsg"

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/3b0168b2-9824-4ef1-a61b-f8f80db3775f">

---

Click on "Inbound Security Rules"

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/2d84d9c4-9f60-4142-baa9-9a215c69b06c">

---

Click on "Add" to create a new Firewall Secuirty rule

<img width="1128" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/a65fa860-deef-4ebb-ace2-13e8a9996435">

---

* Choose the "ICMP" Protocol
* Choose "Deny" Action
* Set "Priority" to 20
* Name the rule "DenyAnyICMPInbound"
* Click "Add/Save"

<img width="439" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/57b20e03-d854-418b-9eef-894b02bea219">

---

Go back to VM1 and type in the following command
* ping 10.0.0.5 -t
* This command continously pings the given IP address

<img width="1067" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/68fd616c-fc06-4035-98a1-5b7066001620">

* VM1 will continue to ping VM2 until VM2's new Firewall rule goes into effect
* When the Firewall rule goes into effect, the ping no longer works and shows the message "Request time out"
* This signals that your Firewall rule is working properly and is successfully blocking ICMP traffic 
* You can remove this Firewall rule by going back to the VM2 Security Rule that was made and switching to the "Allow" action.

---


##  Using SSH protocol to access Linux VM through Windows

SSH stands for Secure Shell Protocol and it is a widely used tool for securely connecting to remote servers and managing them over an unsecured network, such as the internet. It provides a secure way to access and control remote systems and is commonly used for various purposes.

In order to connect to VM2 using VM1, follow these steps:
* Open Powershell on VM1 (Windows Machine)
* Type in "ssh labuser@10.0.05" <- This is the IP address and user name of the Linux machine
* Enter the password that was made for VM2 (Linux Machine)
* Gain acces to VM2 via SSH
  
<img width="614" alt="image" src="https://github.com/DamianPreslyPerera/Azure-Network-Protocols/assets/89204562/e82eb763-69b6-4e51-839d-2ba6a7cf2658">

You now have access to the Linux machine via VM1 through SSH on a powershell terminal.
