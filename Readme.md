This project documents the setup and configuration of Active Directory Domain Services (AD DS) in a lab/virtual environment, including Organizational Unit (OU) structure, Group Policy Objects (GPOs), and policy enforcement testing

The goal of this project was to gain experience and comfort with AD DS as a tool and gain hands on experience with: 

Setting up AD DS and a domain controller on a virtual machine set up with Windows server 2022
Creating Objects/Users in Active directory and assigning Directory groups 
Create network shared folders and assign permissions for specific scopes
Create a logical heirarchy of Organizational units and apply a policy to a specified OU
Create a Client machine and join it to the domain

Enviorment: 
Platform: VMware workstation pro
Domain controller OS: Windows server 2022
Client OS: Windows 11 Education
Domain name: ravigill.local

## 1. After creating a VM with the intention of being the domain controller i first set a static IP and DNS for the machine, as it will be the DNS for connected client machines. 

![Setting Static IP and DNS](images/01.png)

![CMD showing IP after setting](images/02.png)

## 2. Proceeded to install the necessary features to implement AD DS on the OS using the wizard. 

![Adding AD DS to OS](images/03.png)

![Deploying the changes to make the VM into the domain controller](images/04.png)

## 3. Created a user and a group named marketing, and added the user to the group. 

![Creating User](images/05.png)
![Creating Marketing group](images/07.png)

![Adding the newly created user to the marketing group](images/08.png)


## 4. Shared a group called Marketing data on the network, and assigned permissions to the marketing group to view the contents of this folder. 

![Setting up file share on the Marketing data folder](images/09.png)

![Assigning permissions to Marketing group object to view the contents of the Marketing data folder](images/10.png)

![Security permissions showing the Ravigill\Marketing now has permissions to access this folder](images/11.png)


## 5. Created new Organizational units based on locations named Bergen and Oslo. Also created child organizational units for both locations named users and computers.

![Creating First OU](images/12.png)

![Final heirarchy of newly created OU](images/13.png)

## 6. Set up a new VM with windows 11 Education and connected it to the server through the previously created domain controller. 

![Assigning DNS IP on the new client machine to point towards the domain controller](images/14.png)

![Connecting the machine to the ravigill.local domain](images/15.png)

![Providing necessary credentials to connect to the domain. I used administrator, but the user created in step 3 is also possible](images/16.png)

![Confirmation that the domain join was successfull](images/17.png)

![After restarting the client VM it is now part of the domain and since i connected using the admin account it has access to the Marketing Data folder created earlier](images/18.png)

## 7. Moved the now connected Client VM to the Oslo/Computers OU for clarity and easier management

![Client VM now in the correct OU](images/20.png)

## 8. Created a GPO named Test_policy to Oslo/computers OU to force a specific default lock screen and logon image and prevent changing lock screen and logon image. 

![Choosing the policy from Group policy management Editor](images/22.png)

![Created a Image in Paint and the placed it in SYSVOL, then linked the path to the image in the policy rule](images/24.png)

As i was running this homelab on a low resource enviorment i could not make the image properly load, but to confirm that the policy was correctly applied i used the CMD on the cliend VM to see what the OS recognises as the lock screen image.

![CMD output for lock screen image](images/25.png)

