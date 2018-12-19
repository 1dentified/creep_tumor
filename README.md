# Creep Tumor 5.0
## Hardware Setup

Select any server that is capable of support 2 or more virtual machines and at least 2 physical nics.
Recommended hardware components:

Bock Bock|Bock Bock
--------- ---------

##Hardware Setup

Basic setup includes the use of 4 hard drives used for two separate volumes created by the raid controller as follows.

   - Ensure all 4 hard drives are in the server.
   - Turn on the server!
   - Select the appropriate key to enter raid configuration.
   - Delete any current volumes.
   - Create ESXI volume with 2 hard drives and raid 1
   - Create Creep_Tumor volume with 2 hard drives and raid 1
   - Initialize both volumes.
   - Insert Win 10 DVD into server and reboot, booting to DVD drive.
   - Follow the Windows 10 setup only to the select a volume window.
      - In this window select the each raid volume you created and click format.
      - When complete with formating each drive reboot the server and remove the Win10 DVD
   - Insert the ESXi 6.7u1 bootable CD and boot to DVD drive.
   - Follow ESXI installation instructions.

## Network Configuration
On the Switch
   - On the l3 switch create the internal VLAN and VLAN interface for the esxi managment network.
      >conf t 
      >
      
   - Configure the trunk port for vmnic0 or the connected vmnic you will be using for the vmk0 managment int on the ESXi
      >
      

On the ESXi
   - vSwitch0 will automatically assign the vmnic that is plugged in as well as vmk0 to vSwitch0
   - ESXi managment ip needs to be set to an internal IP of your choosing and assign the corret vlan #


