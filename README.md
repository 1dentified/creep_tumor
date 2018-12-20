# Creep Tumor 5.0
## Hardware Setup

Select any server that is capable of support 2 or more virtual machines and at least 2 physical nics.
Recommended hardware components:

   - 4 CPUs
   - 

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
For the rest of the instructions we will be using the following placeholders:
   - Management VLAN: 10
   - Server VLAN: 20 **This should be an existing server VLAN within your network
   - Native Trunking VLAN: 999

On the Switch/Router
   - On the Layer 3 Switch or Router create the internal VLAN and VLAN interface for the esxi managment network.
      ```
      RTR(config)#interface Vlan 10 
      RTR(config-if)#description ESXI Management
      RTR(config-if)#ip address x.x.x.x
      ```
      
   - Configure the trunk port for vmnic0 or the connected vmnic you will be using for the vmk0 managment int on the ESXi
      ```
      RTR(config)#interface [port#/#]
      RTR(config-if)#description Creep Tumor Management
      RTR(config-if)#switchport
      RTR(config-if)#switchport mode trunk
      RTR(config-if)#switchport trunk native vlan 999
      RTR(config-if)#switchport trunk allowed vlan 10
      ```
      
   - Configure the trunk port for the connected vmnic you will be using for the servers
      ```
      RTR(config)#interface [port#/#]
      RTR(config-if)#description Creep Tumor Management
      RTR(config-if)#switchport
      RTR(config-if)#switchport mode trunk
      RTR(config-if)#switchport trunk native vlan 999
      RTR(config-if)#switchport trunk allowed vlan 20
      ```

   - On the ESXi
      - vSwitch0 will automatically assign the vmnic that is plugged in as well as vmk0 to vSwitch0
      - ESXi managment ip needs to be set to an internal IP of your choosing and assigned to VLAN 10


