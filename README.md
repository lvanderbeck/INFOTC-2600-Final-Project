# INFOTC-2600-Final-Project - The installation of FreeNas 
>This project is a tutorial based final for Professor Musser's INFOTC 2600: Digital Multimedia. The topic of this tutorial is a step by step install of the network attached software FreeNas. FreeNas is a free OS to implement the use of data shared over a network, otherwise known as a network attached server (NAS). This tutorial is by Logan VanDerBeck. The target of this tutorial is anyone who is looking for data access and sharing over their network. I would give it a easy difficulty for install and a medium difficulty for full understanding of the ins and outs of FreeNas. It is appropriate for any age who can use a computer and follow directions. 

**Step 1** Download FreeNas  
>FreeNas is a free software available over https://www.freenas.org/download/. *There are a few requirements needed to run a NAS based on FreeNas. You will need a 64-bit CPU and a bare minimum of 8gb of RAM (though more would be greatly beneficial, which is explained later on).*  
The most up-to-date version is 11.1, though other versions are availabe if you'd wish to download an early version.  


**Step 2** Prepare a USB Stick for the the installation media.  
>*FreeNas is downloaded as an ISO which has to be flashed onto a bootable flash drive for installation. The most common way to do this is to use a USB burner such as Rufus. Rufus is available for download over at https://rufus.ie/en_IE.html.*  

Select your boot device (the usb drive), the boot selection (your FreeNas ISO), and your partition scheme (MBR).  
Once you have everything selected, press **Start**. It will then ask you if you would like to erase everything on the USB: click yes.  
  
![Step 2](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/1.png)  
  
**Step 3** Installing FreeNas  
>*To boot into the USB drive, you will need to hit whatever key is needed for the boot menu. Check your motherboard's manual for which key it is, usually F8, F11, or F12.*  
  
Chose to boot from USB to boot into the FreeNas installation screen.  
Choose the FreeNas Installer from the first screen by pressing **Enter**.  

![Step 3](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/2.png)  
  
On the next prompt, choose 1 to Install/Upgrade.  
  
![Step 4](  https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/3.png)
  
You will then need to chose which Hard Drive you want to install FreeNas on.  
  
>*You will need to install FreeNas on a seperate HDD that won't be included in your Hard Disk Array. For my example, I want FreeNas installed on ada0 and my raid set up on ada1 and ada2.*  
  
![Step 5](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/4.png)  

Chose that you are aware everything on the Hard Drive will be wiped. 

![Step 6](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/5.png)

Chose a strong Root password

>*You will use this password to log into the web GUI, so remember it*

![Step 7](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/6.png)
  
 Next, you will need to chose between BIOS or UEFI mode for your boot preference.  
  
 >*If you are not sure, chose boot via BIOS.*  
 
 ![Step 8](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/7.png) 
   
 Finally, let the installer finish installation. Hit **OK** when the installer has finished.  
   
 ![Step 9](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/8.png) 
 
 Select **Reboot System**. remove your USB drive after the restart is done.  
 
 ![Step 10](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/9.png)  
 
 **Step 4** Initial Configuration.  
   
 >*FreeNas runs off a Web GUI as well as a terminal console. After initial installation, you will be shown the console set up. If you have DHCP enabled, it will be given an IP address based off the ranges of your DHCP server. Within the terminal console, it allows you do change settings in the event that your Web GUI is not accessible*    
   
 Make a note of where your web user interface is set. In the example, my web GUI is at http://192.168.100.233  
   
 ![Step 11](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/10.png)
 
 *Optional Step*   
 If you would like a static IP address for your FreeNas box (which I would recommend), choose **1) Configure Network Interfaces)**.  
 Follow the picture below for settings. 
 >*If you have a different default gateway, or would like an IP address different than the one shown, at the **IPv4 Address** enter your IP address you would like FreeNas to use, and at **IPv4 Netmask**, enter the subnet mask used for your default gateway.*  
 
 ![Step 12](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/11.png)
 
 Open up a webpage and head over to the IP address listed on your web user interface.   
 
 ![Step 13](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/12.png)  
 
 **Step 5** Initial Web GUI Configuration.  
 
 Once you login with **root** and your root password you set early, exit out of the configuration wizard. 
 
 Congrats!! You're finally able to set up your first volume and get your NAS up and working on your network.   
 
 **Step 6** Creating a ZFS Volume.  
 
 >*ZFS is a logical volume manager which has continuous integrity and error checking, as well as automatic repair. It is similar to RAID, except it is different in which the controller has access to both the volume manager and the file system. Therefore, it has complete knowledge of both physical disks and volumes, increasing speed and decreasing loss of data due to physical errors. Depending on how big you want your ZFS raid to be, the rule of thumb is to have 1gb of RAM to every TB of storage you would like. This is because the data compression of ZFS takes place in RAM, making it memory hungry. This will be the limiting speed factor to your ZFS NAS. 
 
 Navigate to Storage > Volumes > Volume Manager.  
 
 >*Give your volume a descriptive name. This will help you track multiple volumes later on if you decide to expand or make multiple NAS folders.  
 
 The ZFS Raid set you choose is entirely up to you. I will list some differences between the different choices you can choose, but for my use, I will be using RaidZ.  
 
 >*RaidZ1: You need at least 3 Hard Drives, RaidZ1 is the equivalent of Raid5. It works with parity, if 1 Hard Drive fails, your Data is still there and you can replace the broken Hard Drive. If a second Hard Drive fails at the same time (not unlikely), your Data is lost.
**Usage case:** If you want more storage at the cost of security, data loss acceptable (If you run separate backups of your important data for example).  
RaidZ2: You need at least 4 Hard Drives, RaidZ2 is the equivalent of Raid6. It also works with parity, but 2 Hard Drives can fail before data loss occurs. **Usage case:** Security over storage space. Takes up more storage than RaidZ1.*
 
 Hit save once you are finished with naming, selecting which disks you want in the array, and what type of raid array you would like. 
 
 **Step 7** Creating a User Account for Windows sharing. 
 
 Navigate to Account > Users > Add user. 
 
 >*Fill out everything according to the picture. Username, password are subject to change. Click **Ok** when finished*.
 
 ![Step 14](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/13.png)
 
 **Step 8** Creating a Dataset 
 
 Navigate to Storage > Volumes > /mnt/NameOfVolume (what you named your ZFS volume in step 6)  
 
 >*Datasets are the drives you will create your data on. While the ZFS is in charge of the the data handling with RAID, the dataset will distinguish how your data is shown.  
 
 Give the dataset a name, and select the Share Type (windows), then click **Add Dataset**. 
  
  ![Step 15](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/14.png)  
  
  Click on **Change Permissions** to give access to your user you created in Step 6.   
  
  ![Step 16](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/15.png) 
  
  **Step 9** Creating the Windows Share  
  
  Navigate to Sharing > Windows (SMB) > Shares > Add Windows (SMB) Share.  
  
  Click on **Browse** and slect the dataset you created in Step 8.  
  
  ![Step 17](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/16.png)  
  
  If this is your first share, you will get asked to enable the service. Click **Yes**.  
  
  ![Step 18](https://github.com/lvanderbeck/INFOTC-2600-Final-Project/blob/master/17.png)  
  
  You're all set! Now all you have to do is add the Network Drive on windows, and you can access your NAS anywhere on your network! All you have to do is log in with your credentials you set in step 3. 
  
  
 
 
 




