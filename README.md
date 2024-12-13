# Active Directory Enterprise Lab

This project is a lab setup to simulate an enterprise-level Active Directory (AD) environment using Windows Server 2022 as the Domain Controller and Windows 10 as the client machine. The lab includes walkthroughs for setting up Active Directory, managing users, groups, and organizational units (OUs), and configuring group policies.

## Requirements
- Hyper-V or VMware for virtualization
- Windows Server 2022 ISO
- Windows 10 ISO
- PowerShell for adding users

## Network Diagram

![Active Directory User Topology ](https://github.com/user-attachments/assets/f6b5043e-d69f-4ac7-b8da-8f641d6863fc)


## Setup Guide
- Set up Windows Server 2022 as the Domain Controller (DC):

- Install Active Directory Domain Services (AD DS) on the server.
Promote the server to a Domain Controller.

- The external network will use DHCP to automatically assign an IP address, allowing the server to connect to the internet without manual configuration.
The internal network is currently showing an APIPA address. We will manually configure the internal network’s IP address according to the network diagram above.
We will use CIDR notation (/24) to allocate 254 usable IP addresses for the internal network.
   ![Active Directory User Internal Network Adapter has an APIPA address and needs to be manually changed](https://github.com/user-attachments/assets/3730bc99-d4de-4b62-9842-b8e3bee5d3d9)
   ![Active Directory User Configure AD and add a new forest](https://github.com/user-attachments/assets/57220670-3ce1-4e89-b6c0-d5b760c6c386)
   ![Active Directory User Internal Network Adapter changed to static IP address](https://github.com/user-attachments/assets/6c77e56e-4630-43a1-9dea-809ff735f676)

  ## Create Users

- I have created an OU for Admins and added myself as an Administrator to manage the environment. This allows me to set policies, change passwords, and add or delete users and Organizational Units (OUs).
![Active Directory User Adding an OU with ADMINS and adding myself as a user](https://github.com/user-attachments/assets/185ca10e-d13b-4d78-8438-3e96d4e07c03)

- I used a random name generator to create 1000 unique names and saved them to a text file. Then, I ran a PowerShell script to add these users to my Active Directory environment, simulating a large enterprise setup
![Active Directory User Adding random names to AD](https://github.com/user-attachments/assets/6e24837e-098f-4da9-91f5-90ebb6a67730)
![Active Directory User PowerShell script for adding users](https://github.com/user-attachments/assets/813e18b6-7eb3-4490-889e-054c1102aead)
![Active Directory User New users in AD](https://github.com/user-attachments/assets/6e249cb2-9618-48c6-bb8a-8fa8aedb151b)

## Connect the Windows 10 Client to the internal network 
- Configured the Windows 10 client to obtain its IP address via DHCP from the domain controller, simulating a corporate network environment. 
![Active Directory User Windows 10 IPconfig](https://github.com/user-attachments/assets/697ba645-af93-4c1c-9a1f-fea8eb04ba15)

- Changed the computer name to "CLIENT1" and joined it to the Active Directory domain mydomain.com.
![Active Directory User Changing computer name and adding to mydomain com](https://github.com/user-attachments/assets/1b7aedb9-50e9-421f-8b9a-7667cfe6062f)

- On the Domain Controller, we can view the IP addresses and lease expiration times for all devices on the network via the DHCP management console. 
![Active Directory User DHCP Client address leases](https://github.com/user-attachments/assets/a6f08e2a-6561-4917-8490-957eb2d5963a)

## Conclusion

- We have set up a domain controller that allows any user to connect to the network from any computer, provided they have the proper credentials. 
