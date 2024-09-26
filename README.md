# Active Directory

## Objective

The project aims to explore Active Directory functionality, learn how to ingest events to a SIEM and simulate attack scenarios to develop detection and response capabilities. This hands-on experience was designed to deepen my understanding of setting up a domain environment and monitoring capabilities to help protect it.

### Skills Learned

- Understanding of a domain environment.
- Analyzing and interpreting network logs.
- Ability to recognize attack patterns and signatures.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Active Directory
- Sysmon
- Splunk
- Atomic Red Team

## Steps
<!-- drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Continue to add screenshots and steps as you go.-->
### Building a Diagram

When building a network it is always a good practice to start by building a network diagram. Having a network diagram will allow you to have a reference point for any information you might need down the line, such as IP addressing. After having your diagram setup, I would suggest having at least the hostnames, IP addresses, and domain name added into the diagram. For my diagram I used [draw.io](https://app.diagrams.net/)


![Network Diagram](https://github.com/user-attachments/assets/eccbcc19-c740-420c-9ef7-854d76430ad3)

*Ref 1: My Network Diagram*

### Setting Up Virtual Machines

Next, download the operating system ISOs and programs. For my project I used Windows 10, Windows Server 2022, Kali Linux, and Ubuntu Server. The operating system ISOs will also need a host to run on. Using virtualization software, such as Oracle's VirtualBox, facilitates this by allowing multiple OS instances to run on top of your current OS. **Always download files from the original source!**

Here are links to the official websites to download their products:
- [Windows 10](https://www.microsoft.com/en-us/software-download/windows10)
- [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022)
- [Ubuntu Server](https://ubuntu.com/download/server)
- [Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines)
- [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)

*Do keep note that your computer will need to have the ability to run virtualized OS instances. One way to check is to go open 'Task Manager' and navigate to the 'Performance' tab. If your computer supports virtualization then the 'CPU' section will have a line that says 'Virtualization' and it will either say 'Enabled' or 'Disabled' (in which case you would go to the BIOS to enable it); if you do not see the 'Virtualization' line then your computer does not support virtualization.*

![Checking Virtualization Support](https://github.com/user-attachments/assets/07cfe741-2879-4ccd-bbe5-b016cef3fc48)

*Ref 2: Checking for virtualization support in Windows 11*

Once support for virtualization has been verified and VirtualBox installation has completed, it is time to install the operating systems within VirtualBox. To do this, open VirtualBox and choose the 'New' button to create a new virtual machine. A 'Create Virtual Machine' window pops up to assist you in creating a VM. Under 'Name', give the VM a name to distinguish it from others (this is different than the hostname; VirtualBox-only name). Next, under 'Folder', select where you want to have your VM related files stored (make sure to have enough storage if you want to create snapshots of the VMs; highly recommended). The location of the ISO file of the operating system should be specified under the 'ISO Image' field. Upon locating the ISO file the next four fields that follow should self-populate according to the ISO file chosen. There is an option to 'Skip Unattended Installation' in which VirtualBox attempts to go through the whole installation setup without user intervention. My preference is to go through the installation setup myself, however, you can choose to skip it. This guide assumes manual installation.

Next is specifying how much of the hardware the VM is allowed to use. The values selected here should at least reflect that of the minimum recommendations given by the official distributors of each OS. (Do keep note that the values selected here are *maximums* meaning that the virtual machine will not be using the stated amount at all times). The last step is to create a virtual hard disk (VHD). Select the amount of memory that you want to allocate to the VHD and select finish. 

Here is a list of the hardware settings I allocated to each VM:
- **Windows 10** - 4096 MB Memory | 1 CPU | 50 GB VHD
- **Windows Server 2022** -  4096 MB Memory | 1 CPU | 50 GB VHD
- **Ubuntu Server** - 8192 MB Memory | 2 CPUs | 100 GB VHD
- **Kali Linux** - 2048 MB Memory | 1 CPU | 50 GB VHD

### Installing Windows / Windows Server 2022 / Ubuntu Server / Kali Linux

<!-- Add Windows installation (brief description preferred), maybe include Windows server installation here too. Screenshot? Doesn't seem justifiable as it is really easy but something to think about still. -->
<!-- I actually immediatley changed it after to having a section where all of them are installed. This way if anyone wants to skip the installation section they can easily do so. -->

### Implementing Splunk & Sysmon
<!-- Where do you get splunk? Sysmon? Olaf hartong mention as well. Verify splunk connectivity by reaching it by it's IP address:Port. Image with splunk landing page would be great. -->

### Enabling Active Directory Domain Services (AD DS)
<!-- How to enable it? Show an image of where it is. Feel free to add more images here for AD setup experience. Include the restarting and end with promoting it to a domain controller. -->

### Creating a Domain + Joining a Domain
<!-- Self-explanatory. Don't forget to include how to create users and mentioning the different things you can do here. Feel free to be as in-depth as possible! End with how to verify the joining of a domain (although the login screen is a verification already, lol)-->

<!-- ### Preparing for Telemetry 
(WIP name. As we move forward with the project remember to update this. The main appeal to me of this project is the Active Directory portion.)
I have an idea! Create a new branch (or repository [or whatever it's called]), basically, link the AD part to somewhere else where you will go and explore AD at your own will. Then document your findings and try to create a simulation of your own that might resemble that of an enterprise's domain. If you really want to go for extra credit, set up group policies for the specific groups according to each ones' needs!

