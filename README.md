# INFOTC-2600-Final-Project - The installation of FreeNas 
This project is a tutorial based final for Professor Musser's INFOTC 2600: Digital Multimedia. The topic of this tutorial is a step by step install of the network attached software FreeNas. FreeNas is a free OS to implement the use of data shared over a network, otherwise known as a network attached server (NAS). This tutorial is by Logan VanDerBeck.

**Step 1** Download FreeNas  
FreeNas is a free software available over https://www.freenas.org/download/. *There are a few requirements needed to run a NAS based on FreeNas. You will need a 64-bit CPU and a bare minimum of 8gb of RAM (though more would be greatly beneficial, which is explained later on).*  
The most up-to-date version is 11.1, though other versions are availabe if you'd wish to download an early version.  

**PIC HERE**   
  
  
**Step 2** Prepare a USB Stick for the the installation media.  
*FreeNas is downloaded as an ISO which has to be flashed onto a bootable flash drive for installation. The most common way to do this is to use a USB burner such as Rufus. Rufus is available for download over at https://rufus.ie/en_IE.html.*  
Select your boot device (the usb drive), the boot selection (your FreeNas ISO), and your partition scheme (MBR).  
Once you have everything selected, press **Start**. It will then ask you if you would like to erase everything on the USB: click yes.  
  
**PIC HERE**  
  
**Step 3** Installing FreeNas  
*To boot into the USB drive, you will need to hit whatever key is needed for the boot menu. Check your motherboard's manual for which key it is, usually F8, F11, or F12.*  
Chose to boot from USB to boot into the FreeNas installation screen.  
Choose the FreeNas Installer from th efirst screen by pressing **Enter**.  
**PIC HERE**  
  
On the next prompt, choose 1 to Install/Upgrade.  
**PIC HERE**  
  
You will then need to chose which Hard Drive you want to install FreeNas on. *You will need to install FreeNas on a seperate HDD that won't be included in your Hard Disk Array. For my example, I want FreeNas installed on ada0 and my raid set up on ada1 and ada2.*  
**PIC HERE**  




