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

*Do keep note that your computer will need to have the ability to run virtualized OS instances. One way to check is to go open 'Task Manager' and navigate to the 'Performance' tab. If your computer supports virtualization then the 'CPU' section will have a line that says 'Virtualization' and it will either say 'Enabled' or 'Disabled' (in which case you would go to the BIOS to enable it). If you do not see the 'Virtualization' line then your computer does not support virtualization.*
![Checking Virtualization Support](https://github.com/user-attachments/assets/07cfe741-2879-4ccd-bbe5-b016cef3fc48)

*Ref 2: Checking for virtualization support in Windows 11*

Once support for virtualization has been verified and VirtualBox installation has completed, it is time to install the operating systems within VirtualBox. To do this, open VirtualBox and choose the 'New' button to create a new virtual machine. A 'Create Virtual Machine' window pops up to assist you in creating a VM. Under 'Name', give the VM a name to distinguish it from others (this is different than the hostname; it is a VirtualBox-only name). Next, under 'Folder', select where you want to have your VM related files stored (make sure to have enough storage if you want to create snapshots of the VMs, which is highly recommended). The location of the ISO file of the operating system should be specified under the 'ISO Image' field. Upon locating the ISO file the next four fields that follow should self-populate according to the ISO file chosen. There is an option to 'Skip Unattended Installation' in which VirtualBox attempts to go through the whole installation setup without user intervention. My preference is to go through the installation setup myself, however, the option to skip manual installation is there.

Next is specifying how much of the hardware the VM is allowed to use. The values selected here should at least reflect that of the minimum recommendations given by the official distributors of each OS. (Do keep note that the values selected here are *maximums* meaning that the virtual machine will not be using the stated amount at all times). The last step is to create a virtual hard disk (VHD). Select the amount of memory that you want to allocate to the VHD and select finish. 

Here is a list of the hardware settings I allocated to each VM:
- **Windows 10** - 4096 MB Memory | 1 CPU | 50 GB VHD
- **Windows Server 2022** -  4096 MB Memory | 1 CPU | 50 GB VHD
- **Ubuntu Server** - 8192 MB Memory | 2 CPUs | 100 GB VHD
- **Kali Linux** - 2048 MB Memory | 1 CPU | 50 GB VHD

### Installing Windows / Windows Server 2022 / Ubuntu Server / Kali Linux
<!-- Add Windows installation (brief description preferred), maybe include Windows server installation here too. Screenshot? Doesn't seem justifiable as it is really easy but something to think about still. -->
<!-- I actually immediatley changed it after to having a section where all of them are installed. This way if anyone wants to skip the installation section they can easily do so. -->
<!-- Fork[?] (is this the term?) these installation steps onto another file. This is to reduce image bloat here and keep the focus on the Active Directory portion.-->
<!-- Solution thought up! Add a brief explanation here and then link to a page in where you provide more detailed instructions! Genius! -->
<!-- Make sure to include somewhere within there on how to setup the NAT Network. Specifically, set it up for use within our lab 
     Don't forget to include how to setup each machine's IP address to correspond to our diagram! ! ! -->

### Implementing Splunk in Ubuntu Server
<!-- Where do you get splunk? Sysmon? Olaf hartong mention as well. Verify splunk connectivity by reaching it by it's IP address:Port. Image with splunk landing page would be great. -->
<!-- Currently, I'm thinking about removing the Cyber Sec stuff to focus on AD for now. As a result, this will stay empty for now. -->

On the host machine (not the VMs) go to [splunk.com](https://www.splunk.com) and sign up for an account to log in. Once logged in, go under the tab labeled 'Products' and select 'Free Trials & Downloads'. A page will load with different products. The one we are interested in right now is 'Splunk Enterprise' so click on the 'Get My Free Trial' button below it. When presented with the download page, make sure to click on the 'Linux' tab and download the '.deb' file by selecting the 'Download Now' option beside it. Save the file to the directory of your choice; I saved it to a folder dedicated to this project.

For the next step, some additional add-ons will be needed on the Ubuntu Server for VirtualBox. In the Ubuntu Server, type `sudo apt-get install virtualbox-guest-additions-iso` and press enter. Type 'y' for yes and press enter. This will take some time to complete. You may be asked to select or confirm the restarting of some services in which you can just press enter. Once you see that some services have restarted you'll know that the process has finished.

Go to the menu options at the top of the VirtualBox window and select 'Devices' > 'Shared Folders' > 'Shared Folders Settings'. Add a new folder by selecting the icon of a folder with a plus sign, located on the right side. For the 'Folder Path' select the directory in where you stored the Splunk installer. For example, if I stored my Splunk installer under "D:\Active-Directory-Project" then I would choose this location as the folder path. A 'Folder Name' should automatically fill in when a path is selected, which is fine. Make sure to fill the three options labeled: 'Read-only', 'Auto-mount', and 'Make Permanent'. Click 'Ok'. Back on the VM type `sudo reboot` to reboot the machine.

When prompted, type in the username and password. Now we want to add our user to the vboxsf group. To do this type `sudo adduser username vboxsf` (replace 'username' with the username you use to login!) and press enter. Type in your password to proceed. A message might appear with the message "The group 'vboxsf' does not exist". In that case we will need additional guest installations that VirtualBox offers thaht we did not install yet. Type `sudo apt-get install virtualbox-guest-utils` and hit enter. Type `sudo reboot` to reboot the system. Once logged in you should able to add the user to the vboxsf group using the steps mentioned previously.

Next, we'll create a folder named 'share'. To do this we'll type `mkdir share` and press enter. You can verify the creation of this directory by entering the `ls` command. Now we will mount or shared folder onto the directory named 'share'. We'll do this by entering the command `sudo mount -t vboxsf -o uid=1000,gid=1000 sharefoldername share/` (replace 'sharefoldername' with the name of *your* shared folder name). For example, if my share folder name is 'Active-Directory-Project' then I would enter the command `sudo mount -t vboxsf -o uid=1000,gid=1000 Active-Directory-Project share/`. We can verify the success of our command by entering `ls -la` and seeing our 'share' folder highlighted. Note that if an error appears after entering the command to mount our shared folder then you may need to exit the session using `exit` and log back in to have the previous changes we made to take effect.

We can now change directories into our 'share' folder. To do this input the command `cd share/`. Inputting the `ls -la` command will list any files stored in this directory, including our Splunk installer. To install Splunk, input `sudo dpkg -i splunk`, hit tab (to autofill the rest of the filename), and then press enter. The process of installing Splunk will begin automatically; we will verify completion upon seeing the word 'complete' displayed on-screen.

To start Splunk we will change directories to where Splunk is located using the `cd /opt/splunk` command. If we use the `ls -la` command we will notice all of the user and group belong to 'splunk'. This limits the permissions to that of the user (splunk). If it were set to root, it would run under root privileges, which would be a security concern as it does not need that many privileges. Let's continue under the user 'splunk'. To do this we will enter the command `sudo -u splunk bash` which will let us act as the user 'splunk'.

As the 'splunk' user we'll go to the bin directory using `cd bin` and then input the `./splunk start` command which will run the installer. A terms and agreement page will appear; scroll through the agreement and type 'y' for yes to accept. Next type and administrator username that you will use to log into Splunk and create a corresponding password. We can verify completion upon the installer telling us where the Splunk web interface is located. The location will be at the server's IP address using port 8000.

The final thing we want is for Splunk to automatically run every time we turn on this machine. First, exit out of the 'splunk' user by using `exit` and then change directories to 'bin' using `cd bin`. We will type `sudo ./splunk enable boot-start -user splunk` and press enter to send the command. This makes it so that Splunk will run under the user 'splunk' any time that the system reboots and, finally, our Ubuntu server is now officially a Splunk server.

### Implementing Sysmon and Universal Forwarder in Windows 10 / Server 2022
<!-- added due to the length of the previous section; too big if I add splunk+sysmon steps together -->
<!-- the asteriks are there because I might start sending the troubleshooting sections to to other pages to reduce text bloat and keep a clean and organized page structure. This also allows for pictures for the troubleshooting help. -->

Switching over to the Windows 10 Pro machine, let's make note of the IP address. Head over to the command prompt and input `ipconfig` and press enter. You'll find your machines address in the 'IPv4 Address' section. The reason we are checking here is to make sure that the IP address leased does not conflict with the static IP address we have noted for our other machines in our network diagram. <!-- ** --> 
If it does, we can work around this by giving the machine a static IP address separate from other machines. To do this, right click on the internet connection at the bottom left and select 'Open Network & Internet settings'. The settings window will appear and we'll select 'Change adapter options' and then right-click on the adapter and choose 'Properties'.  Double-click on 'Internet Protocol Version 4 (TCP/IPv4) and select 'Use the following IP address' to statically assign an IPv4 address to this machine. You can type any IP address that will not be used by any other machines as long as it is in the 192.168.10.0/24 domain. The subnet mask is 255.255.255.0, default gateway will be 192.168.10.1 and the DNS server can be Google's public DNS server at 8.8.8.8. Go to the command prompt and type the same command as before and we should see our IP address updated to confirm our changes.

*Note: Ideally, there should be reserved IP addresses with the leaseable IP addresses being specifically marked as available. However, this has been omitted in this project for simplicity as the focus will be on Active Directory and Splunk. For more information on how to setup reserved IP addresses/DHCP pools check out my page on it -> [filler page](https://github.com/HolyYewfelle)* <!-- make a page later. more experience/blog-like posts is great! -->

Open an internet browser within the VM and attempt to connect to the Splunk server. The server's IP address is the one specified earlier at 192.168.10.10:800. This opens up the portal to log into Splunk. That's great! Now, still inside the VM, we'll head over to splunk.com and login using our same credentials as earlier. We'll navigate to 'Products' > 'Free Trials and Downloads' and select the free download of 'Universal Forwarder'. We'll select the 64-bit option of Windows and download it. Once it's downloaded [let's go through the UniversalForwarder Setup](https://github.com/HolyYewfelle) <!-- make page later! -->

While Universal Forwarder finishes installing we can go ahead and download Sysmon. Search 'sysmon' in the web browser and the Microsoft Sysmon page should appear. Within that page we can click on 'Download Sysmon' to begin the download. The sysmon configuration we'll be using is by a user 'olaf hartong' and should easily appear with a simple search of 'sysmon olaf hartong config'. Make sure the webpage name mentions sysmon-modular. Go through the github files and select the 'sysmonconfig.xml' file. Once open, click on 'Raw' on the right side and then right-click to save the raw file as 'sysmonconfig.xml'. Open File Explorer and view the Downloads section. There should be the 'Sysmon' zip file we recently installed and the 'sysmonconfig' XML file as well. Right-click and select extract to unzip the 'Sysmon' zip file. Once it is completed, go to PowerShell as an administrative user and change directory into the 'Sysmon' folder (`cd C:\Users\username\Downloads\Sysmon` with `username` being the name of the user you created on this machine). Once inside the directory, input the command `.\Sysmon64.exe -i ..\sysmonconfig.xml` to begin installing Sysmon after agreeing to the EULA.

Universal Forwarder should have finished installing by this point. This next part is an important one as we will specify what we want Universal Forwarder to send to our Splunk server. What we want to do here is create a file named inputs.conf inside of `C:\Program Files\SplunkUniversalForwarder\etc\system\local`. To do this we will open Notepad with administrator priveleges, [copy this into notepad](https://github.com/HolyYewfelle), <!-- insert file contents page --> and save it as 'inputs.conf' under the path mentioned while making sure the 'Save as type' field is set to 'All Files'. Whenever the 'inputs.conf' file is updated we must restart the service for Splunk Universal Forwarder. To do this search for 'Services' in the Windows search bar and, inside of the Services window, find 'SplunkForwarder'. You may notice the service is set to log on as 'NT SERVICE' so, if that happens, we want to double-click on the name, switch to the 'Log On' tab, select the 'Local System account' option and then hit 'Apply'. We will be informed that we will need to reset the service, which is what we are doing. To restart the service make sure that SplunkForwarder is highlighted and then click on 'Restart the service' on the left side. If you get a dialogue window, close it out and click on 'Start the service'. With Sysmon and Universal Forwarder setup, we are now ready to finalize our Splunk server configuration.

Connect to the Splunk server at 192.168.10.7:8000 and log in using the username and password provided when installing Splunk. Once logged in, we want to go under 'Settings' and select 'Indexes'. If you recall the configuration file earlier, we had an index labeled 'endpoint' and we are now going to create it within Splunk. Click on 'New Index' and give the index the name of 'endpoint'. Click on 'Save' and we should see our new index within the list. Next we will configure the Splunk server to receive data. Go to 'Settings' > 'Forwarding and receiving' > 'Configure receiving' > 'New receving port' and input the default port we setup earlier of 9997. If everything was setup correctly, we should now see data coming from our Windows 10 machine. To verify this, go to 'Apps' > 'Search & Reporting' and we'll input 'index=endpoint' into the search bar and click on the search button. If we have data showing then that means we can verify that everything has been set up correctly.

Now repeat the process for installing Universal Forwarder and Sysmon within Windows Server 2022. I renamed the Windows Server to 'ADDC-01', as naming conventions are typically employed within an enterprise's network. If you want to change the name you can go to 'Settings' > 'System' > 'About' > 'Rename this PC'.

<!-- Idea page format
[Paragraph 1] ... If you need to change your IP address then check how to do so [here](link_to_troubleshoot_page).
[Paragraph 2] Next, we'll [setup our Splunk universal forwarder](link_to_installation_page). Once it's running we can proceed to download Sysmon. We'll go to here.com and do this.... (explain)
-->



### Enabling Active Directory Domain Services (AD DS) + Creating a Domain
<!-- How to enable it? Show an image of where it is. Feel free to add more images here for AD setup experience. Include the restarting and end with promoting it to a domain controller. -->
Steps to enable and set up as a domain controller

Windows Server comes with an application called 'Server Management'. To create a domain, we first must enable Active Directory Domain Services (AD DS). We can do so by going under 'Manage' and selecting 'Add Roles and Features'. We'll skip the introductory page and in the 'Installation Type' section we'll make sure that 'Role-based or Feature-based installation' is selected before proceeding. In the 'Server Selection' section we will select the server in which we want to install AD DS; I selected ADDC-01 as my server, for example. It is on the next page that AD DS is listed and we will select it and accept the extra features that are required for AD DS. For our purposes we will then skip the next pages until we reach the confirmation screen. Upon confirming that we have selected the right features, we can then click on 'Install'. We can verify completion once a progress report containing the words "Installation succeeded" appears under the progress bar. 

Upon closing out the feature installation window, we will notice an icon has appeared on the flag symbol. This is where our notification messages appear and, if we click on it, we'll notice an option of promoting the server to a domain controller (DC). We will click on that and immediately select 'Add a new forest' to create a brand new domain. Our domain will need a root domain name in the form of a FQDN (Fully Qualified Domain Name). Using the name of my domain as an example (kotone), the root name of my domain will be `kotone.local`. On the next page, we will leave the defaults and create a password. This may be a lab environment but best practices is to make sure that this password is secure! We will leave the defaults for the next few pages as well. Take a quick look at the review page to verify changes. There will be a prerequisites check before you will be able to install; select 'Install' when able to do so. The machine should prompt for a restart, which we will accept.

After restarting, our login screen will immediately verify our success. Our 'Administrator' user should now be lead with backslash and the name of the domain that we just created; my admin login was `KOTONE\Administrator`. The server now has AD DS installed and has been promoted to a DC. Cheers!

### Creating Users + Organizing Users by Department
<!-- Self-explanatory. Don't forget to include how to create users and mentioning the different things you can do here. Feel free to be as in-depth as possible! End with how to verify the joining of a domain (although the login screen is a verification already, lol)-->

Once the domain is created, the next step is to start creating some users. Let's log in and do that now. In our 'Server Manager' application we will navigate to 'Tools' and select 'Active Directory Users and Computers'. This tool allows us to create objects, which is the collective term used to describe users, computers, and groups to name a few examples. Expanding the domain will reveal some folders. The 'Builtin' folder will show us all of the groups automatically created by Active Directory. Within this folder, we can view information, such as the description, by double-clicking the name of a group. The description and name are listed in the 'General' tab while 'Members' indicates who is a member of this group. The 'Members Of' group displays any groups that the selected group is a part of; built-in groups cannot be members of other groups but a custom group can be a part of a built-in group.

Moving on, the 'Users' folder will contain a list of users, along with additional groups. We can create additional users and groups within this folder, which by the way is called an 'OU' or 'organizational unit'; however, in a real-world environment the users are likely broken up into different departments through the use of OUs. Creation of OUs are done by right-clicking the domain and navigating to 'New' > 'Organizational Unit'. Let's create our first OU and name it 'IT'. We can use this to create users for an IT department! We can create as many OUs as we like and can even create them within an OU. For example, I could create an OU within 'IT' named 'Managers' which would house any users/groups pertaining to management within our IT department.

I'm going to create a new user for our IT department by right-clicking a blank area within our IT OU and navigating to 'New' > 'User'. I will give the user a first name of "Jenny" and a last name of "Smith"; the user logon name will be "jsmith". Having a user logon naming convention of "[first name initial]+[last name]" is standard for many enterprises. I will create a password for this user on the next page. Notice the option that says 'User must change password at next logon'. For our lab environment, we can disable this option; however, keep in mind that it is best practice to always have this enabled in a real-world scenario. I'll proceed to the next screen and verify the information before selecting 'Finish'. I now have a user inside of 'IT' named Jenny Smith. I will be creating additional users and OUs for additional departments; use the previous steps to create as many as you wish.


### Joining a Domain
<!-- felt better to separate this to keep a more organized layout? Depending on how long this section is I may reorganize the AD portion later. As always, just writing current thoughts for future reference. -->

<!-- ### Preparing for Telemetry 
(WIP name. As we move forward with the project remember to update this. The main appeal to me of this project is the Active Directory portion.)
I have an idea! Create a new branch (or repository [or whatever it's called]), basically, link the AD part to somewhere else where you will go and explore AD at your own will. Then document your findings and try to create a simulation of your own that might resemble that of an enterprise's domain. If you really want to go for extra credit, set up group policies for the specific groups according to each ones' needs!

