# **Born2beRoot Guide**

by Anton Ferrus (Git)@afmyhouse (42)antoda-s

# The Virtual Machine

## How does a virtual machine work and what is its purpose:

A virtual machine is an application that emulates a whole computer and runs inside a physical computer. It works as a separate independent machine, but it runs as a process on an host operating system. It’s a convenient way to dedicate a portion of a computer's resources to a specific task or software.

Virtual machines are used to dedicate a portion of a host’s resources to a specific task. This machine will run in an isolated environment without any risks of conflicting with the host. If the guest virtual machine crashes, it can be rebooted or recovered without impacting the host.

## The basic differences between Rocky Linux 8 and Debian 11 Bullseye:

## **It’s a Server Use Case**

Debian and Rocky Linux options are excellent options for server OS

* **Debian** is a distribution known for its penchant of choosing **stability over anything else**.  
* **Rocky Linux 8** is designed to be a **server system**

  ## 

  ## **Server Use Case**

    
  If I’m part of the camp that is looking for a distribution that I would like to use to run my applications on as a server, then **Debian and Rocky Linux are excellent options**   
  **Debian** is known to care about the stability of the applications it ships with and thus guarantees that my server and applications running on it are “okay” technically.   
  **Rocky Linux** is designed to be a server system, hence gaming, media and similar programs aren’t necessarily all there by default. However, much like with Fedora or CentOS, I can enable a set of third-party repositories to gain access to these additional applications and utilities.

## 

  ## **Desktop Use Case**


  Debian 11 and Debian 10 **ship with plenty of desktop features** . We only need to download and install the desktop that we would wish to have and off I go.


  Rocky Linux on the other end comes with GNOME as the default desktop. It does not mean that other flavors are absent but the user will have to install them on their own. If we look to Install our own desktops, Rocky is the option.

  Debian 11 and Debian 10 do a better job in this arena compared to **Rocky Linux 8 which is more biased towards server usage**. **Moreover, in case I still have a 32 bit computer** lying around in a cellar somewhere, Debian 11 is happy to keep it alive and kicking. **Debian has consistently continued to support 32 bit** architecture and this should be good news for those with old 32 bit systems lying around.


## My choice of operating system:

**Debian 11**. I’m very familiar with this version as I’m an experienced RPI user and it uses a special compilation of the debian, the version raspbian. It also seemed much easier to set up for the purpose of this 42 project, considering the subject specs.

## Debian 11 x Rocky Linux 8

| Feature   | Debian 11 | Rocky Linux 8.4 |
| :---- | :---- | :---- |
| Release Date | August 14th, 2021 | June 21st, 2021 |
| Code Name | Bullseye | Green Obsidian |
| Kernel | Features Kernel 5.10 LTS | Features Kernel 4.18.0-305 |
| 32 bit support	 | Still supports 32 bit | Does not support 32 bit |
| Desktop Flavors | GNOME 3.38, KDE Plasma 5.20, LXDE 11,  LXQt 0.16, MATE 1.24, Xfce 4.16 | Rocky Linux 8 has GNOME as the default desktop environment. Other environments /flavors such as  KDE, Xfce need to be  installed by the user. |
| Based on | The mother of many descendant operating systems such as Ubuntu | Based on RHEL |
| Packet Filtering  More on note \[A\] | Uses nftables  | Nftables Replaces iptables |
| AppArmor/SELinux  More on note \[B\] | AppArmor enabled per default | SELinux enabled per default |
| exFAT | Bullseye is the first release providing a Linux kernel which has support for the exFAT filesystem | exFAT filesystem not supported out of the box.  I have to install a package |
| Package Manager  More on note \[C\] | apt | Yum, DNF |
| My option | Debian 11 |  |

1. ## **nftables**

   ## **https://wiki.debian.org/nftables**

     
   **nftables** Is the new framework by the Netfilter Project, allowing to perform packet filtering (firewalling), NAT, mangling and packet classification. **nftables** is the replacement for **iptables**. There are some tools in place to ease this task. Please read: [https://wiki.nftables.org/wiki-nftables/index.php/Moving\_from\_iptables\_to\_nftables](https://wiki.nftables.org/wiki-nftables/index.php/Moving_from_iptables_to_nftables)  
     
   Check **nftables** status:

| `me-user@me-user42$> sudo systemctl status nftables.service [sudo] password for me-user: ● nftables.service - nftables  	Loaded: loaded (/lib/systemd/system/nftables.service; disabled; vendor preset: enabl>  	Active: inactive (dead)    	Docs: man:nft(8)          	http://wiki.nftables.org` |
| :---- |

   

2. ## **AppArmor vs. SELinux** 

   ## **(https://phoenixnap.com/kb/apparmor-vs-selinux)**

     
   Both **SELinux** and **AppArmor** provide security tools that isolate applications and limit access to an attacker that has compromised one part of the system.  
   

   1. ## **AppArmor**

   

   **AppArmor** works by granting access first, then applying restrictions. **AppArmor**  is a practical [Linux security](https://phoenixnap.com/kb/linux-security) module that has been included by default with [Ubuntu](https://phoenixnap.com/kb/ubuntu-22-04-lts) since version 7.10. The module allows developers to restrict applications from using specific files. Hence, **AppArmor** prevents any damage to potentially vulnerable applications and protects easy-to-exploit software, like web servers. The module uses **security profiles** to determine **what permissions** the application requires. Profiles are text files loaded into the kernel, typically on boot.

**AppArmor** enforces two main types of rules in profiles:

- **Path entries.** 		They determine which files an application can access.  
- **Capability entries.** 	These rules specify the privileges a confined process is allowed to use.

**AppArmor** Profiles are designed to confine specific apps and they work in two modes. In the

- **Complain mode**. In this mode, the system reports policy violation attempts but does not enforce rules.  
- **Enforce mode**. In Enforce mode, the new profile is inspected and all violations are stopped.

**AppArmor** consists of the following components:

- **Server analyzer.** Scans ports and locates applications listening to them automatically. It also detects applications without profiles and those that AppArmor needs to confine.  
- **Profile generator.** A static process that analyzes applications and creates a profile template.  
- **Optimizer.** This component logs and gathers events into the profile of normal behavior.

Apart from Ubuntu, AppArmor runs on Debian, SUSE Enterprise Server, OpenSUSE distributions, and other distributions by default. 

## 

2. ## **Advantages of AppArmor**

   

   The main advantages of AppArmor are the simplicity and short learning curve. This module is **far less complex than SELinux,** making it easier to set up and manage.

   The tool works directly with **profiles (text files)** for access control, and file operations are more straightforward. This feature makes **AppArmor more user-friendly than SELinux** with its security policies.

   Thanks to the path-based implementation, AppArmor **protects any file on the system and allows for rules to be specified even for files that do not exist yet.** The program's learning mode makes AppArmor adaptable to changes and **enforces preferred application behavior**.

   3. ## **Drawbacks of AppArmor**

   

   With AppArmor, **more than one path can refer to the same application**. These different paths to the same executable create multiple profiles for one app, which **is a potential security issue**.

   

   Furthermore, AppArmor's greatest strength, **simplicity, is also why the program is considered less secure**.

   

   **AppArmor** doesn't have Multi-Level Security (MLS) and Multi-Category Security (MCS). **The lack of MCS support makes AppArmor almost ineffective in environments requiring MLS**. 

   

   Another drawback is that the policy loading also takes longer, so the **system starts up slower**.

   

   4. ## **Check AppArmor module status**

| `me-user@me-user42$> sudo apparmor_status [sudo] password for me-user: apparmor module is loaded. 3 profiles are loaded. 3 profiles are in enforce mode.    lsb_release    nvidia_modprobe    nvidia_modprobe//kmod 0 profiles are in complain mode. 0 processes have profiles defined. 0 processes are in enforce mode. 0 processes are in complain mode. 0 processes are unconfined but have a profile defined.` |
| :---- |

## 

   The output shows that **AppArmor** is active on the system. The command also prints the list of installed profiles and the active confined processes.

   

3. ## **SELinux**

     
   **SELinux**,  restricts access to all applications by default and grants access only to users that present the proper certifications. **SELinux** assigns labels to the system's files, processes, and ports. Label type is vital for targeted policies, while type enforcement is the second most crucial concept in SELinux. Labeling serves as a grouping mechanism that gives files and processes different types of labels. The type enforcement security model helps SELinux determine whether a process with a particular label type has access to a file with another label type.  
     
   The system restricts access by default (as opposed to AppArmor). Users must be properly configured to access any resource.  
     
   SELinux cashes previous decisions in the Access Vector Cache (AVC), for example, allowing or restricting access. Cashing decisions speeds up the access control process. For instance, if an application tries to access a file, SELinux checks against the AVC and permits or denies access based on the previous decision.  
     
   RHEL, CentOS, and Fedora have SELinux installed or available by default.   
   

   1. ## **Advantages of SELinux**

   

   Despite (and due to) the complex policies, SELinux is considered the more secure option for Linux security.

   

   Labeling and type enforcement allow SELinux to grant access only if a policy rule allows it. This process implements a more robust and in-depth access control.

   By being MLS-compatible, SELinux offers better access features. For instance, one of the basic MLS principles is that users can only read files at their sensitivity level and lower. However, with SELinux, sysadmins can read and write files at their own and lower sensitivity levels. 

   By default, the system separates files from each other and the host and maintains the separation. For instance, a file has different sets of permissions for:

   

* The owner (user).  
* A group holding the file.  
* Other users/groups accessing the file.


  2. ## **Drawbacks of SELinux**


  SELinux provides sysadmins with a versatile access control tool. However, this security module has some disadvantages.

  SELinux is quite difficult to learn, set up, and manage. While the program efficiently controls access to applications and files, troubleshooting potential issues is difficult for beginners. It is not always easy to determine what an error message actually means and where to look for the issue. Overall, SELinux is not user-friendly and non-experienced admins may face a steep learning curve.


  **Check SELinux module status**

| `me-user@me-user42$> sudo sestatus [sudo] password for me-user: sudo: sestatus: command not found` |
| :---- |

## **The result makes sense as the OS is Debian and not RL8**

3. ## **Conclusion AppArmor versus SELinux**

   

   Both systems offer different approaches to Linux security and protect machines against unauthorized access and modification of system resources.

   

   we might want to learn about other ways to protect our system, like using [immutable backups](https://phoenixnap.com/kb/immutable-backups) to fight ransomware or different procedures for [database protection.](https://phoenixnap.com/kb/database-security)

   

4. ## **\[3\] apt and aptitude**

   ## **(https://blog.packagecloud.io/know-the-difference-between-apt-and-aptitude/)**

   1. ## **What is apt** 

   [Apt](https://wiki.debian.org/Apt) is the default Linux command-line tool to manage the packages on a Debian-based system. It comes by default and doesn't offer a graphical interface to manage the tools that are installed and the ones that we may need in the future. To install a package, we need to specify the name of the package just after the \`apt install\` command. The package manager reads the \`/etc/apt/sources.list\` file and the contents of the \`/etc/apt/sources.list.d\` folder to retrieve the ones that we need with all the dependencies.

   Apt command offers a lot of sub-commands that help us to manage our system so that the packages can be added, updated, removed, or fixed if a problem occurs. During those processes, it will automatically install, update or remove the necessary dependencies or the other packages which depend on the main package that is being operated

   ## **What is aptitude ​**

[Aptitude](https://www.debian.org/doc/manuals/aptitude/rn01re01.en.html) is another popular tool that we can use over apt. It offers a command-line and text-based front-end for package management. It doesn't come by default, so we need to install it with the \`apt\` command. aptitude offers the possibility to manage our packages through command lines and also from a visual interface directly on our terminal. We can perform the main actions like installing, updating, and deleting our packages. it also offers sub-commands to manage our packages as apt but some people prefer the visual interface as it's easy to use.

## **Let's understand the difference** 

If we consider only the command-line interfaces of each, they are quite similar as each of them offers us different ways to manage our packages. Therefore, there are a few differences that we can list:

- Apt offers a command-line interface, while aptitude offers a visual interface  
- When facing a package conflict, \`apt\` will not fix the issue while \`aptitude\` will suggest a resolution that can do the job  
- aptitude can interactively retrieve and displays the Debian changelog of all available official packages  
  ​Apt requires the user to have a solid knowledge of Linux systems and package management as we are running everything in the command line. It can be difficult for a novice to handle.  
  On the other hand, aptitude with its interface is more user-friendly as it offers a layer of abstraction regarding the different sub-commands to use for installation, upgrades, etc.

  ## 

  ## **To conclude apt versus aptitude**

  Now we know the difference between apt and aptitude. \`aptitude\` works as an alternative to \`apt\` and offers a multiple-choice dependency resolution that can is useful. aptitude is more for novice users while apt can be considered for people with a good understanding of Linux package management. There are also some other [package managers](https://blog.packagecloud.io/5-best-linux-package-managers/) that we have on the other [popular Linux distributions](https://blog.packagecloud.io/10-most-popular-linux-distributions-and-why-they-exist/).

5. ## **\[3\] DNF and  Yum**

   ## **(https://docs.rockylinux.org/en/books/admin\_guide/13-softwares/\#dnf-dandified-yum)**

**What is DNF: Dandified Yum**

**DNF** (Dandified Yum) is a software package manager, successor of **YUM** (Yellow dog Updater Modified). It works with RPM packages grouped in a local or remote repository (a directory for storing packages). For the most common commands, its usage is identical to that of yum.

The **dnf** command allows the management of packages by comparing those installed on the system with those in the repositories defined on the server. It also automatically installs dependencies, if they are also present in the repositories.

**dnf** is the manager used by many RedHat based distributions (RockyLinux, Fedora, CentOS, ...). Its equivalent in the Debian world is APT (Advanced Packaging Tool).

The dnf command allows us to install a package by specifying only the short name.

| `me-user@me-user42:~# dnf [install][remove][list all][search][info] package` |
| :---- |

Example:

| `me-user@me-user42:~# dnf install tree` |
| :---- |

# Simple Setup verifications

## Login

- [ ] **Log to Virtual Machine as a created user**

Don’t log  as root ( with the purpose of future generic use of this document as a reference for any other debian setup, the generic user will be referenced as  me-user  instead of the  real user , hence username \= me-user) when  me-user  is used it should be replaced with the user created. Also the hostname is a concatenation of ‘me-user’ \+ ‘42’ \=\>  me-user42 .  

| `me-user42 login: me-user Password:**********` |
| :---- |

## Operating System

- [ ] **Check the operating system:**

| `me-user@me-user42:~# hostnamectl | grep Operating | awk -F: '{print $2}' Debian GNU/Linux 11 (bullseye)` |
| :---- |

| Note `about this command pipeline` |
| :---- |

| `me-user@me-user42:~# hostnamectl   Static hostname: me-user42         Icon name: computer-vm           Chassis: vm        Machine ID: 805dea4d9d144963990712dc7fe6dad4           Boot ID: b7669b9e688542bbb224eff9582e84a5    Virtualization: oracle  Operating System: Debian GNU/Linux 11 (bullseye)            Kernel: Linux 5.10.0-21-amd64      Architecture: x86-64 me-user@me-user42:~# hostnamectl | grep Operating  Operating System`: `Debian GNU/Linux 11 (bullseye)  me-user@me-user42:~# hostnamectl | grep Operating | awk -F: '{print $2}' Debian GNU/Linux 11 (bullseye)` |
| :---- |

## Password policy

- [ ] **Verify password validity policy**   
      

| `me-user@me-user42:~# sudo chage -l me-user Last password change                                  : May 02, 2023 Password expire                                       : Jun 01, 2023 Password inactive                                     : never Account expires                                       : never Minimum number of days between password change        : 2 Maximum number of days between password change        : 30 Number of days of warning before password expires     : 7` |
| :---- |

## Firewall

- [ ] **Check UFW service status.**

| `me-user@me-user42:~# sudo ufw status Status: active To                     	Action  	From --                     	------  	---- 4242                   	ALLOW   	Anywhere             	  80                     	ALLOW   	Anywhere             	  21                     	ALLOW   	Anywhere             	  4242 (v6)              	ALLOW   	Anywhere (v6)        	  80 (v6)                	ALLOW   	Anywhere (v6)        	  21 (v6)                	ALLOW   	Anywhere (v6)`   	 |
| :---- |

## SSH

- [ ] **Check SSH service is started.**

| `me-user@me-user42:~# sudo systemctl status ssh ● ssh.service - OpenBSD Secure Shell server        Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)        Active: active (running) since Thu 2023-05-04 14:27:07 WEST; 3h 5min ago        Docs:   man:sshd(8)                man:sshd_config(5)        Process: 569 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)        Main PID: 616 (sshd)        Tasks: 1 (limit: 1125)        Memory: 6.8M        CPU: 100ms        CGroup: /system.slice/ssh.service          	└─616 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups May 04 14:27:07 me-user42 systemd[1]: Starting OpenBSD Secure Shell server... May 04 14:27:07 me-user42 sshd[616]: Server listening on 0.0.0.0 port 4242. May 04 14:27:07 me-user42 sshd[616]: Server listening on :: port 4242. May 04 14:27:07 me-user42 systemd[1]: Started OpenBSD Secure Shell server. May 04 14:28:11 me-user42 sshd[748]: Accepted password for me-user from 10.11.10.14 port 49564 ssh2 May 04 14:28:11 me-user42 sshd[748]: pam_unix(sshd:session): session opened for user me-user(uid=1000) by (uid=0)` |
| :---- |

## Hostname

- [ ] **Check** the hostname of the machine is correctly formatted as follows: me-user42 

| `me-user@me-user42:~# hostnamectl me-user42` |
| :---- |

- [ ] **Modify** this hostname by replacing the login with ours, then restart VM.

| `me-user@me-user42:~# sudo hostnamectl set-hostname new_hostname me-user@me-user42:~# sudo reboot` |
| :---- |

- [ ] **Modify** this hostname by editing and change the name of the host at the /etc/hostname file

| `me-user@me-user42:~# sudo nano /etc/hostname me-user@me-user42:~# sudo reboot` |
| :---- |

	**Note**:	If on restart, the hostname has not been updated, the evaluation stops here.

- [ ] **Restore** the machine to the original hostname, then restart VM.

## Partitions

- [ ] How to view the partitions for the VM :

| `me-user@me-user42:~# lsblk NAME                	MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT sda                   	8:0	  0 30.8G  0  disk   ├─sda1                	8:1	  0  500M  0  part  /boot ├─sda2                	8:2	  0    1K  0  part   └─sda5                	8:5	  0 30.3G  0  part     └─sda5_crypt      	254:0	  0 30.3G  0  crypt 	├─LVMGroup-root 	254:1	  0   10G  0  lvm   / 	├─LVMGroup-swap 	254:2	  0  2.3G  0  lvm   [SWAP] 	├─LVMGroup-home 	254:3	  0    5G  0  lvm   /home 	├─LVMGroup-var  	254:4	  0    3G  0  lvm   /var 	├─LVMGroup-srv  	254:5	  0    3G  0  lvm   /srv 	├─LVMGroup-tmp  	254:6	  0    3G  0  lvm   /tmp 	└─LVMGroup-var--log 254:7	  0    4G  0  lvm   /var/log sr0                  	11:0	  1 1024M  0  rom` |
| :---- |

- [ ] Compare the output with the example given in the subject (if there are bonuses, refer to the bonus example).

## 

## LVM Partitions

**What is the advantage of using LVM?**  
LVM, Logical Volume Manager. The main advantages of LVM are **increased abstraction, flexibility, and control**. Logical volumes can have meaningful names like “databases” or "root-backup”. Volumes **can also be resized dynamically** as space requirements change, and migrated between physical devices within the pool on a running system or exported.

**What are the disadvantages of LVM?**  
One of the drawbacks of using LVM is complexity. LVM adds an extra layer of management and configuration to our storage system, which can make it more difficult to understand and troubleshoot.

**LV \- Logical Volumes**  
Logical volumes are **groups of information located on physical volumes**. A hierarchy of structures is used to manage disk storage. Each individual disk drive, called a physical volume (PV) has a name, such as /dev/hdisk0. Every physical volume in use belongs to a volume group (VG).

**VG \- Volume Groups**	  
Volume groups are collections of physical volumes. It is the next level of abstraction in LVM. Volume groups are the storage pool that combines the storage capacity of multiple physical  storage devices.  
**PV \- Physical Volumes**  
The LVM allows for the use of disk space regardless of the physical volumes. Physical volumes are the devices itself where the LVM strategy will be implemented.

## USERS 

- [ ] an user with the login of the student being evaluated

| `me-user@me-user42:~# getent passwd me-user. me-user:x:1000:1000:me name,,,:/home/me-user:/bin/bash` |
| :---- |

\*should match the user to fetch and verify

- [ ]  it has been added and that it belongs to “sudo” group

| `me-user@me-user42:~# getent group sudo sudo:x:27:me-user,user42-2` |
| :---- |

- [ ]  it has been added and it belongs to the “user42” group.

| `me-user@me-user42:~# getent group user42 user42:x:1001:me-user,user42-1,user42-2` |
| :---- |

## 

# SETUP : sudo

## Foreword

*`sudo`*, which is an acronym for *superuser do* or *substitute user do*, is a command that runs an elevated prompt without a need to change our identity. Depending on our settings in the `/etc/sudoers` file, we can issue single commands as root or as another user. To continue running commands with root power, we must always use the *sudo* command. 

## Why not always just use su instead?

Becoming root permanently with `su` is a well-known 'no-no' in the \*nix universe. Why? Because becoming root with `su` means that we are root, which is the same as logging into a terminal as the root user with root's password. And that's dangerous for many reasons. So to avoid this we shall install the sudo package wich provides many tools to bring safety to the root actions including make one aware of the command line instruction by forcing the use of the *sudo* command before any other command

## Recapping what I've learned.

* `sudo` lets issue commands as another **user** without changing its identity  
* The **user** needs an entry in `/etc/sudoers` to execute these restricted permissions  
* `sudo -i` brings an interactive session as root  
* `su` means to switch to a particular user  
* Just typing `su` switches to the root user  
* `sudo` will ask for current user password, while `su` will ask for the password for the user whom to switching to

## Additional Commands used in this chapter

In this chapter I had the chance to use several bash commands in so many different ways. The following are the commands and its basic synopsys from my point of interpretation that I used in this SUDO chapter.

| command | most common use | description |
| :---- | :---- | :---- |
| su su \- | switch to root switch to root including environment | su Is an acronym for **switch user or substitute user**. It’s basically switching to a particular user and the password is needed for the user switching to.  Most often, the user account we switch to is the root account but it can be any account on the system. [https://www.redhat.com/sysadmin/difference-between-sudo-su](https://www.redhat.com/sysadmin/difference-between-sudo-su) |
| sudo sudo \-i | super user do super user start  interactive session | sudo stands for either “substitute user do” or “super user do” . What sudo does is incredibly important and crucial to many Linux distributions. Effectively, sudo allows a user to run a program as another user (most often the root user). There are many that think sudo is the best way to achieve “best practice security” on Linux.  [https://www.redhat.com/sysadmin/difference-between-sudo-su](https://www.redhat.com/sysadmin/difference-between-sudo-su) |
| dpkg | **dpkg** \-l | grep sudo | The dpkg is a tool to install, build, remove and manage Debian packages. [The dpkg Command in Linux \- A Beginners Reference | DigitalOcean](https://www.digitalocean.com/community/tutorials/dpkg-command-in-linux) |
| apt | apt install \<package name\> apt-get apt-upgrade  | APT stands for Advanced Packaging Tool. The command line apt is a package manager and provides options for searching and managing as well as querying information about packages. It provides the same functionality as the specialized APT tools, like apt-get and apt-cache, but enables options more suitable for interactive use by default. It is an open-source tool, which means we can use it without the need to pay anything. APT is designed to handle software installation and removal. APT was part of Debian’s .deb package; however, it was updated to work with the RPM Package Manager. If we have used APT before, we would have noticed that it is a command-line tool. This means we need to use commands to work with it with no visual reference from a graphical interface(the initial plan was to include a graphical interface, but the idea was later dropped). To use it, we need to provide the package name. The package should have its sources specified in the ‘/etc/apt/sources.list.’ It should also contain all the dependencies list that the package needs to install automatically. If we use the apt command, it will not only download and install the required dependencies for the said package. As a user, we do not have to worry about the package dependencies. The approach taken by APT is flexible. This means that the user can configure how APT works, including adding new sources, providing upgrade options, and so on\! With time, APT showed improvements on how it can be handled. Also, Debian developers are in full control of how it gets updated. |
| usermod | usermod \-aG user group  | The usermod command can be used for performing a lot of things related to users and groups, using flags. This command is specifically designed for Linux users to update and change anything regarding other users in their existing system. |

	

1. **Install sudo**

   

- ## **Login as super user and change to root environment:**

| `me-user@me-user42$> su - Password: *********` |
| :---- |

## **\*\*\*\*\*   this is the root password  \*\*\*\*\***

### 

- ## **Install sudo using atp so the package manager install the required packages for sudo**

| `root@me-user42:~# apt install sudo` |
| :---- |

- ## **reboot  to apply changes.** 

| `root@me-user42:~# sudo reboot` |
| :---- |

- ## **After reboot, check if sudo is installed properly and its version**

| `me-user@me-user42:~# sudo -V Sudo version 1.9.5p2 Sudoers policy plugin version 1.9.5p2 Sudoers file grammar version 48 Sudoers I/O plugin version 1.9.5p2 Sudoers audit plugin version 1.9.5p2`  |
| :---- |

- ## **If the result is too large, it may be saved to a *file***

| `me-user@me-user42:~# sudo -V > sudo_version_file.txt` |
| :---- |

  ## 	\[info added to file.txt\]

- ## **Check that the “sudo” program is properly installed on the virtual machine.**

| `me-user@me-user42:~# dpkg -l | grep sudo ii  sudo                         	1.9.5p2-3+deb11u1 [...]` |
| :---- |

  2. **Adding / Deleting** **users and groups**

- ## **Add myself to *sudo* group after reboot (myself is me-user)**

| ``me-user@me-user42:~# sudo adduser me-user sudo Adding user `me-user' ... Adding new group `me-user' (1004) ... Adding new user `me-user' (1003) with group `me-user' ... Creating home directory `/home/me-user' ... Copying files from `/etc/skel' ... New password:``  |
| :---- |

- ## **Create group *user42***

| `me-user@me-user42:~# sudo addgroup user42` |
| :---- |

### 

- ## **Check if group *user42* was created**

| `me-user@me-user42:~# getent group user42` User42:x:1001:me-user |
| :---- |

- ## **Create user *user42-1* and Check if user *user42-1* was created**

| `me-user@me-user42:~# sudo adduser user42-1 me-user@me-user42:~# id user42-1` uid=1003(user42-1) gid=1004(user42-3) groups=1004(user42-1) |
| :---- |

- ## **Add user *user42-1* to group *user42***

| `me-user@me-user42:~# sudo adduser user42-1 user42` |
| :---- |

- ## **or** 

| `me-user@me-user42:~# usermod -aG user42 user42-1` |
| :---- |

- ## **Create and Add user user42-2 to group *user42* and check group *user42***

| `me-user@me-user42:~# sudo adduser user42-2 me-user@me-user42:~# sudo adduser user42-2 user42 me-user@me-user42:~# getent group user42 User42:x:1001:me-user,user42-1` |
| :---- |

- ## **Add user user42-2 to group *user42* and check group *user42***

| `me-user@me-user42:~# sudo adduser user42-2 user42 me-user@me-user42:~# getent group user42 User42:x:1001:me-user,user42-1, user42-2` |
| :---- |

- ## **How *to check created users?***

| `me-user@me-user42:~# less /etc/passwd me-user@me-user42:~# more /etc/passwd me-user@me-user42:~# cat /etc/passwd me-user@me-user42:~# cat /etc/passwd | grep ‘/home/bash/’ > users.txt` |
| :---- |

When using less:  use q to exit if needed

- ## **Delete user user42-2**

| `me-user@me-user42:~# getent passwd user42-2 user42-2:x:1005:1007,,,:/home/user42-2:/bin/bash me-user@me-user42:~# sudo deluser user42-2 me-user@me-user42:~# getent passwd user42-2 user42-2:x:1001:,user42-1 me-user@me-user42:~# cat /etc/passwd | grep ‘/home/bash/’ > users.txt` |
| :---- |

- ## **Remove user *user42-2* from group *user42***

| `me-user@me-user42:~# sudo deluser user42-2 me-user@me-user42:~# getent group user42 user42:x:1001:me-user,user42-1` |
| :---- |

  3. **Rules for SUDO**

The implementation of the rules imposed by the subject

- ## **Create a dir to log where each command will be logged, the input and the output**

| `me-user@me-user42$> mkdir /var/log/sudo` |
| :---- |

- ## **Create a file to store the sudo policy**

| `me-user@me-user42$> touch /etc/sudoers.d/sudo_config` |
| :---- |

| `Defaults  passwd_tries=3 Defaults  badpass_message="me-user says there is something wrong with our password" Defaults  logfile="/var/log/sudo/sudo_log" Defaults  log_input, log_output Defaults  iolog_dir="/var/log/sudo" Defaults  require tty Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"` |
| :---- |

  4. **The implementation of the rules imposed by the subject:** 

- ## **use *visudo* command to edit the /etc/sudoers file**

| `me-user@me-user42$> sudo visudo` |
| :---- |

- **Verify the “/var/log/sudo/” folder exists and has at least one file.** 

| `me-user@me-user42$> sudo ls -lap /var/log/sudo/` |
| :---- |


- **Check the contents of the files in the folder.**  
- **we should see a history of the commands used with sudo.**

  5. **Check further, for example :**  
- **Run a command via sudo.**   
- **See if the file(s) in the “/var/log/sudo/” folder have been updated.**  
  


2. ## **PASSWORD policy**

#### Foreword

There are two sets of definitions for the password that have to be configured properly: Expiry policy and composition/quality

1. **Expiry policy**

**First set** of definitions is about the expire policy of the password validity and its related 

- \<minimum number of days\> between a password change   
- \<days to expire\> warning  
- \<maximum days\> of duration

- **The expire policy is defined at login definitions editing the respective file \-  /etc/login.defs \-  accordingly.**

| `me-user@me-user42$> sudo nano /etc/login.defs` |
| :---- |

- **Those are the parameters that need to be changed accordingly:**

| `# Password aging controls: # #   	PASS_MAX_DAYS   Maximum number of days a password may be used. #   	PASS_MIN_DAYS   Minimum number of days allowed between password changes. #   	PASS_WARN_AGE   Number of days warning given before a password expires. # PASS_MAX_DAYS   9999 PASS_MIN_DAYS   0 PASS_WARN_AGE   7` |
| :---- |

- **Change the following settings on the /etc/login.defs file:** 

| `# Password aging controls: # #   	PASS_MAX_DAYS   Maximum number of days a password may be used. #   	PASS_MIN_DAYS   Minimum number of days allowed between password changes. #   	PASS_WARN_AGE   Number of days warning given before a password expires. # PASS_MAX_DAYS   30 PASS_MIN_DAYS   2 PASS_WARN_AGE   7` |
| :---- |

| Existing users' passwords won’t be affected by this edition To apply or edit changes of the expiry policy to existing users: |
| :---- |

- **To edit max days till password expiration**

| `me-user@me-user42$> sudo chage -M 30 me-user` |
| :---- |

- **To edit min days till password change**

| `me-user@me-user42$> sudo chage -m 2 me-user` |
| :---- |

- **To edit warning days before the password expires**

| `me-user@me-user42$> sudo chage -W 7 me-user` |
| :---- |

- **Or, the following command will allow to interactively change or keep any of the above parameters and more**

| `me-user@me-user42$> sudo chage -i me-user Changing the aging information for me-user Enter the new value, or press ENTER for the default         Minimum Password Age [2]:         Maximum Password Age [30]:         Last Password Change (YYYY-MM-DD) [2023-04-12]         Password Expiration Warning [7]:         Password Inactive [-1]:         Account Expiration Date (YYYY-MM-DD) [-1]: me-user@me-user42$>`  |
| :---- |

- **Check EXPIRY POLICY for a \<user\>:**

| `me-user@me-user42$> sudo chage -l me-user Last password change                                           : Apr 12, 2023 Password expires                                               : May 12, 2023 Password inactive                                              : never Account expires                                                : never Minimum number of days between password change                 : 2 Maximum number of days between password change                 : 30 Number of days of warning before password expires              : 7 me-user@me-user42$>` |  |
| :---- | ----- |

  2. **Password content policy**

**Second set** of definitions is about the composition and size of the password

- minimum **10 characters** password length  
- at least one **upper case** character  
- at least one **lower case** character  
- at least one **digit**  
- maximum 3 **consecutive identical** characters  
- reject the **username** alike chain of chars in the password  
- minimum **7 different characters** from previous password  
- This rules **enforce for the root** password

- **Before continuing a password management, the libpam-pwquality package hast to be installed**

| `me-user@me-user42$> sudo apt install libpam-pwquality -y` |
| :---- |

### 

- **To implement the password format policy the password management file \-  /etc/pam.d/common-password \-  must be edited**

| `me-user@me-user42$> sudo nano /etc/pam.d/common-password` |
| :---- |

- **The following line needs to be edited to add the rules for the password construction rules)**

| `# here are the per-package modules (the "Primary" block) password        requisite	pam_pwquality.so retry=3`  |
| :---- |

- **Edit it and change it to include the following at the same line after “retry=3”**   
  **(without breaking the line\!\!)**

| `# here are the per-package modules (the "Primary" block) password        requisite	pam_pwquality.so retry=3  minlen=10 lcredit=-1 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root `  |
| :---- |

| Where: |
| :---- |
| `minlen=10		: minimum password length ucredit=-1		: at least one upper case character dcredit=-1		: at least one digit lcredit=-1		: at least one lower case character maxrepeat=3		: maximum number of consecutive identical chars reject_username	: reject the username alike chain of chars in the password difok=7			: minimum 7 chars different from previous password enforce_for_root	: enforce this rules for the root password` |

| Existing users' passwords won’t be affected by this edition Only at any password change the above rules must be complied |
| :---- |

- **Create a new user (e.g. user42-x) to try out the rules:**

| `me-user@me-user42$> sudo adduser user42-x New password:` |
| :---- |

### 

- **Or change the password of an existing user me-user :**

| `me-user@me-user42$> sudo passwd me-user New password:` |
| :---- |

- **Try to assign a password,**  
  *  **\*\*\* disregarding \*\*\* the rules and verify what happens**  
  * **\*\*\* regarding \*\*\* the rules and verify what happens** 

3. ## **SSH**

   1. **Install SSH**

   

- **Login, as a *super user*, (any *super user*…)**  
- **Install openssh-server using apt**

| `me-user@me-user42$> sudo apt install openssh-server` |
| :---- |

- **Check ssh service status**

| `me-user@me-user42$> sudo service ssh status` |
| :---- |

- **Edit ssh configs files** 

| `me-user@me-user42$> sudo nano /etc/ssh/ssh_config` |
| :---- |

**`/etc/ssh/ssh_config`**  
File **ssh\_config**:   
configuration file for the outgoing communications, the **ssh** client on the host machine we are running. For example, if we want to ssh to another remote host machine, we use a SSH client.   
Every setting for this SSH client will be using ssh\_config, such as port number, protocol version and encryption/MAC algorithms.

| … \#   StrictHostKeyChecking ask \#   IdentityFile \~/.ssh/id\_rsa \#   IdentityFile \~/.ssh/id\_dsa \#   IdentityFile \~/.ssh/id\_ecdsa \#   IdentityFile \~/.ssh/id\_ed25519    Port 4242 \#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc \#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com \#   EscapeChar \~ \#   Tunnel no \#   TunnelDevice any:any \#   PermitLocalCommand no … |
| :---- |

- **Edit sshd configs files** 

| `me-user@me-user42$> sudo nano /etc/ssh/sshd_config` |
| :---- |

  File **sshd\_config**: configuration file for the **sshd** daemon (the program that listens to any incoming connection request to the ssh port) on the host machine. 

  That is to say, if someone wants to connect to our host machine via SSH, their SSH client settings must match our sshd\_config settings in order to communicate with we, such as port number, version and so on.

| … \# The strategy used for options in the default sshd\_config shipped with \# OpenSSH is to specify options with their default value where \# possible, but leave them commented.  Uncommented options override the \# default value. Include /etc/ssh/sshd\_config.d/\*.conf  Port 4242 \#AddressFamily any \#ListenAddress 0.0.0.0 \#ListenAddress :: … |
| :---- |

  2. **Check SSH**


  What is SSH and the added value of using it:  it uses a secure shell, that allows 2 computers to securely talk to each other


- **Check that the SSH service is properly installed on the VM, and is working properly.**

| `me-user@me-user42$> sudo nano /etc/ssh/sshd_config ● ssh.service - OpenBSD Secure Shell server  	Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: e>  	Active: active (running) since Mon 2023-05-08 12:43:00 WEST; 38min ago    	Docs: man:sshd(8)          	man:sshd_config(5) 	Process: 575 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)    Main PID: 623 (sshd)   	Tasks: 1 (limit: 1125)  	Memory: 7.1M     	CPU: 127ms  	CGroup: /system.slice/ssh.service          	└─623 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups` |
| :---- |

- **Verify that the SSH service only uses port 4242\.**

| `me-user@me-user42$> sudo grep -i port /etc/ssh/sshd_config | grep -v Gate Port 4242 #GatewayPorts no me-user@me-user42$> sudo grep -i port /etc/ssh/ssh_config | grep -v Gate Port 4242` |
| :---- |


- **Login remotely to the host me-user42.**

| `anyother-user@anyother-host$> ssh me-user@ip_address -p 4242`   |
| :---- |


- **Use SSH in order to log in with the newly created user.**   
  To do this, we can use a key or simple password, depending on the student being evaluated.

- **Make** **sure we cannot use SSH with the “root” user as stated in the subject.**  
    
- **Close the port 68**

| `me-user@me-user42$> sudo nano /etc/network/interfaces` |
| :---- |

| `# This file describes the network interfaces available on our system # and how to activate them. For more information, see interfaces(5). source /etc/network/interfaces.d/* # The loopback network interface auto lo iface lo inet loopback # The primary network interface allow-hotplug enp0s3 iface enp0s3 inet dynamic`  |
| :---- |

| `# This file describes the network interfaces available on our system # and how to activate them. For more information, see interfaces(5). source /etc/network/interfaces.d/* # The loopback network interface auto lo iface lo inet loopback # The primary network interface allow-hotplug enp0s3 #iface enp0s3 inet dynamic iface enp0s3 inet static    	 address 10.11.248.218    	 netmask 255.255.0.0    	 gateway 10.11.1.1 `  |
| :---- |


  To do this, 

  While the IP attribution is done via DHCP, the port 68 will remain open as it is the port used for the gateway to attribute an IP to the requesting machine with active DHCP option.


  Changing the settings from dynamic to static wil avoid the port 68 opening 68\.

  Hence all IP the settings must be configured at the interfaces file we can use a key or simple password, depending on the student being evaluated.

**UFW**

- [ ] Check the “UFW” program is properly installed on the VM and works properly.

**sudo ufw status numbered**

- [ ] Ask the student for a basic explanation of UFW and the value of using it.  
- [ ] List the active rules in UFW. A rule must exist for port 4242\.  
- [ ] Add a new rule to open port 8080\. Check that this one has been added by listing the active rules.

**sudo ufw allow 8080**

- [ ] Delete this new rule with the help of the student being evaluated.

**sudo ufw delete 4**  
**sudo ufw delete 2**

**ss \-tunlp**

**Netid	State 	Recv-Q	Send-Q   	Local Address:Port   	Peer Address:Port	Process**      
**tcp  	LISTEN	0     	80           	127.0.0.1:3306        	0.0.0.0:\***             	   
**tcp  	LISTEN	0     	1024           	0.0.0.0:80          		0.0.0.0:\***             	   
**tcp  	LISTEN	0     	128            	0.0.0.0:4242        		0.0.0.0:\***             	   
**tcp  	LISTEN	0     	128                 \*:21                		\*:\***             	   
**tcp  	LISTEN	0     	1024              \[::\]:80             		\[::\]:\***             	   
**tcp  	LISTEN	0     	128               	\[::\]:4242           		\[::\]:\*** 	

**SCRIPT**

Create a script **monitoring.sh** that will display, when executed, the required system information.   
The script must start with the command  wall \-n  followed by  “text to display”   
We are going to build the script step by step to define how to build the **text to display**.

- **Architecture**  
  For the architecture of the SO to be shown: This command prints all information, except if the CPU or the hardware platform is unknown.

| `me-user@me-user42$> uname -a Linux me-user42 5.10.0-21-amd64 #1 SMP Debian 5.10.162-1 (2023-01-21) x86_64 GNU/Linux` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "Architecture     : $(uname \-a)” |
| :---- |

- ## **Physical Cores**

For the number of physical cores to be shown we will use the file /proc/cpuinfo, which gives us information about the CPU: its type, brand, model, performance, etc. 

| `me-user@me-user42$> grep "physical id" /proc/cpuinfo | wc -l 4` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "Architecture     : $(uname \-a)               CPU physical    : $(grep 'physical id' /proc/cpuinfo | wc \-l) |
| :---- |

- ## **Virtual Cores**

To show the number of virtual cores is very similar to the previous one. We will again use the file /proc/cpuinfo, but with the filter grep processor 

| `me-user@me-user42$> grep processor /proc/cpuinfo | wc -l 4` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l) “ |
| :---- |

- ## **RAM**

To show the RAM memory we will use the command free with “mega” flag as request by the subject.

| `me-user@me-user42$> free -m                total        used        free      shared  buff/cache   available Mem:            7838        5940         249         797        1648         800 Swap:           2047        2047           0` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "       Architecture    : $(uname \-a)         CPU physical    : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU            : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage    : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}') “ |
| :---- |

- ## **Disk memory**

To view the occupied and available memory of the disk, we will use the df command, which stands for "disk filesystem",  to get a complete summary of the use of disk space.   
As indicated in the subject, the used memory is shown in MB, so we will then use the \-m flag. 

Next, we will do a grep to only show us the lines that contain "/dev/" and then we will do another grep with the \-v flag to exclude lines that contain "/boot".   
Finally, we will use the awk command and sum the value of the third word of each line to once all the lines are summed, print the final result of the sum. 

| `me-user@me-user42$> df -m | grep "/dev/" | grep -v "/boot" | awk '{memory_use += $3} END {print memory_use}'` |
| :---- |

To obtain the total space, we will use a very similar command. The only differences will be that the values we will sum will be $2 instead of $3 (parameter 2 instead of parameter 3\) and the other difference is that in the subject the total size appears in Gb, so as the result of the sum gives us the number in Mb we must transform it to Gb, for this we must divide the number by 1024 and remove the decimals.

| `me-user@me-user42$> df -m | grep "/dev/" | grep -v "/boot" | awk '{memory_use += $2} END {print memory_use}'` |
| :---- |

Finally, we must show a percentage of the used memory. To do this, again, we will use a command very similar to the previous two. The only thing we will change is that we will combine the two previous commands to have two variables, one that represents the used memory and the other the total. Once we have done this, we will perform an operation to obtain the percentage use/total\*100 and the result of this operation will be printed as it appears in the subject, between parentheses and with the % symbol at the end. 

| `me-user@me-user42$> df -m | grep "/dev/" | grep -v "/boot" | awk '{use += $3} {total += $2} END {printf("(%d%%)\n"), use/total*100}'` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}') ” |
| :---- |

- ## **CPU usage percentage**

To view the percentage of CPU usage, we will use the vmstat command, which shows system statistics, allowing us to obtain a general detail of the processes, memory usage, CPU activity, system status, etc.   
We could put no option but in my case I will put an **interval of seconds from 1 to 4**. We will also use the tail \-1 command, which will allow us to produce the output only on the last line, so of the 4 generated, only the last one will be printed.   
Finally, we will only print word 15, which is the available memory usage. 

| `me-user@me-user42$> vmstat 1 4 | tail -1 | awk '{print 100-$15}'` |
| :---- |

The result of this command is only part of the final result since there is still some operation to be done in the script for it to be correct. What should be done is to subtract the amount returned by our command from 100, the result of this operation will be printed with one decimal and a % at the end and the operation will be finished.

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}') " |
| :---- |

- ## **Last reboot**

To see the date and time of our last restart, we will use the who command with the \-b flag, as this flag will display the time of the last system boot on the screen.   
As has happened to us before, it shows us more information than we want, so we will filter it and only show what we are interested in, for this we will use the awk command and compare if the first word of a line is "system", the third word of that line will be printed on the screen, a space, and the fourth word. 

| `me-user@me-user42$> who -b | awk '$1 == "system" {print $3 " " $4}'` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}') " |
| :---- |

### 

### 

- ## **LVM active**

To check if LVM is active or not, we will use the lsblk command, which shows us information about all block devices (hard drives, SSDs, memories, etc) among all the information it provides, we can see lvm in the type of manager.   
For this command we will do an if because we will print Yes or No. Basically, the condition we are looking for will be to count the number of lines in which "lvm" appears and if there are more than 0 we will print Yes, if there are 0 we will print No. 

| `me-user@me-user42$> if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}')         LVM use                : $(if \[ $(lsblk | grep "lvm" | wc \-l) \-gt 0 \]; then echo yes; else echo no; fi) " |
| :---- |

- ## **TCP connections**

To check the number of established TCP connections, we will use the ss command replacing the now obsolete netstat. We will filter with the \-ta flag so that only TCP connections are shown. Finally, we will do a grep to see those that are established as there are also only listening and close with wc \-l to count the number of lines. 

| `me-user@me-user42$> ss -ta | grep ESTAB | wc -l` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}')         LVM use                : $(if \[ $(lsblk | grep "lvm" | wc \-l) \-gt 0 \]; then echo yes; else echo no; fi)         Connections TCP : $(ss \-ta | grep ESTAB | wc \-l) " |
| :---- |

- ## **Number of users**

We will use the users command which will show us the names of the users there are, knowing this, we will put wc \-w to count the number of words in the command output. 

| `me-user@me-user42$> users | wc -l` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}')         LVM use                : $(if \[ $(lsblk | grep "lvm" | wc \-l) \-gt 0 \]; then echo yes; else echo no; fi)         Connections TCP : $(ss \-ta | grep ESTAB | wc \-l)         User(s) logged     : $(users | wc \-l) " |
| :---- |

- ## **IP address & MAC**

To obtain the host address, we will use the hostname \-I command and to obtain the MAC, we will use the ip link command which is used to show or modify the network interfaces. As more than one interface, IP's etc. appear, we will use the grep command to search for what we want and thus be able to print only what is requested.   
To do this, we will put $2 and in this way we will only print the MAC.

| `me-user@me-user42$> ip link | grep "link/ether" | awk '{print $2}'` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}')         LVM use                : $(if \[ $(lsblk | grep "lvm" | wc \-l) \-gt 0 \]; then echo yes; else echo no; fi)         Connections TCP : $(ss \-ta | grep ESTAB | wc \-l)         User(s) logged     : $(users | wc \-l)         Network               : $(hostname \-I ) $(ip link | grep 'link/ether' | awk '{printf("(%s)", $2)}') " |
| :---- |

- ## **Number of commands executed with sudo**

To obtain the number of commands executed with sudo, we will use the journalctl command, which is a tool that is responsible for collecting and managing the system logs.   
Next, we will put \_COMM=sudo in order to filter the entries by specifying its path.   
In our case we put \_COMM because it refers to an executable script.   
Once we have filtered the search and only the sudo logs appear, we still need to filter a bit more as when we start or close the root session it also appears in the log, so to finish filtering we will put a grep COMMAND and this will only show the command lines.   
Finally, we will put **`wc -l`** so that the lines are numbered.   
The entire command is as follows: `journalctl _COMM=sudo | grep COMMAND | wc -l`   
To check that it works correctly, we can run the command in the terminal, put a command that includes sudo and run the command again and it should increase the number of sudo executions.

| `me-user@me-user42$> journalctl -q _COMM=sudo | grep COMMAND | wc -l` |
| :---- |

Add this line to the monitoring.sh script:

| wall \-n "                Architecture           : $(uname \-a)         CPU physical         : $(grep 'physical id' /proc/cpuinfo | wc \-l)         vCPU                      : $(grep 'processor' /proc/cpuinfo | wc \-l)         Memory Usage     : $(free \--mega |awk '$1 \== "Mem:" {printf("%d/%dMB (%.2f%%)",$3,$2,$3/$2\*100)}')         Disk Usage            : $(df \-m | grep "/dev/" | grep \-v "/boot" | awk '{use \+= $3} {total \+= $2} END {printf("%d/%dGb (%d%%)\\n"),use,total/1024,use/total\*100}')         CPU load               : $(vmstat | tail \-1 | awk '{printf("%.1f\\n",100-$15)}')         Last boot               : $(who \-b | awk '$1 \== "system" {print $3 " " $4}')         LVM use                : $(if \[ $(lsblk | grep "lvm" | wc \-l) \-gt 0 \]; then echo yes; else echo no; fi)         Connections TCP : $(ss \-ta | grep ESTAB | wc \-l)         User(s) logged     : $(users | wc \-l)         Network               : $(hostname \-I ) $(ip link | grep 'link/ether' | awk '{printf("(%s)", $2)}')         Sudo                     : $(journalctl \-q \_COMM=sudo | grep COMMAND | wc \-l) " |
| :---- |

Refs:  
[https://kloudvm.medium.com/simple-bash-script-to-monitor-cpu-memory-and-disk-usage-on-linux-in-10-lines-of-code-e4819fe38bf1](https://kloudvm.medium.com/simple-bash-script-to-monitor-cpu-memory-and-disk-usage-on-linux-in-10-lines-of-code-e4819fe38bf1)  
[https://www.cyberciti.biz/faq/what-does-the-sleep-command-do-in-linux/](https://www.cyberciti.biz/faq/what-does-the-sleep-command-do-in-linux/)

Review questions:

- [ ] How does the script work?.

Script inputted in the monitoring .sh file to display system information  
**cd /usr/local/bin && vim monitoring.sh**

- [ ] What is “cron”?  
- [ ] How does the script run every 10 minutes from when the server starts?  
- [ ] Once correct functioning of the script is verified, make sure the script runs with dynamic values correctly.

**sudo crontab \-u root \-e (\*\*\*change 10 value to 1\*\*\*)**

- [ ] Make the script stop running when the server has started up, without modifying the script itself. To check this, restart the VM.

**sudo cronstop**  
**sudo cronstart**

- [ ] At startup, check if the script still exists in the same place, the rights have remained unchanged and that it has not been modified.

| $\> sudo reboot |
| :---- |

| $\> sudo crontab \-u root \-e |
| :---- |

Postposting a scrip a certain amount of time:

### `sleep $(who -b | awk -F : '{printf "%d", $2%10}') && ls` 

## 

## **The ls will only run after sleep  amount of time in seconds, this command Delays the ls for the amount of $time (in seconds)**

## 

### `$> sleep $time && ls`

### 

### `$> sleep ($time)m && ls`Delays the ls for the amount of $time (in minutes)

Example

### `who -b | awk -F' ' '{printf "%s", 45}' | awk -F: '{printf "%d\n", $2%10}'`

Step by step:

### `who -b`

### `system boot 2023-03-15 14:53`

who | awk \-F : '{printf "%d", $2%10}'

$\> who  
Antonio  console  Mar  9 15:18 

$\> who | awk \-F : '{printf "%d", $2%10}'  
8

Explanation:  
$\> who | awk \-F : '{printf "%d", **$2%10**}'  
Antonio  console  Mar  9 15**:18** \>\>\>\>\> **18 % 10 \= 8**

sleep $(who \-b | awk \-F : '{printf "%d", $2%10\*10}') && ls

**ls** will execute after 10 x the digit of minute at reboot (in seconds)  
$\> who \-b  
reboot		\~	10:26

$\> who \-b | awk \-F : '{printf "%d", $2%10\*10}'  
10 X 6 \= 60 secs 

| \*/10 \* \* \* \* sleep $(who \-b | awk \-F: ‘{printf(“\\%d”), $2\\%10}’)m && sh /home/me-user/monitoring.sh  |
| :---- |

### `$> lscpu | grep "CPU(s)" | grep -v "On-line" | awk -F: '{printf("%d\n",$2)}'`

**CLI resumed : MANDATORY START HERE**

`sudo    su –`  
`apt update`  
`apt upgrade`  
`apt install sudo`  
`systemctl status sudo`  
`dpkg -l | grep sudo`

`adduser <username> sudo`  
`( usermod -aG sudo <username>)`

`getent group sudo`

`reboot (para ativar)`  
`sudo -V`

`sudo nano /etc/sudoers.d/<newsudorules>`  
\* Defaults passwd\_tries=3  
\* Defaults badpass\_message=”\<custom-error-message\>”  
\* Defaults logfile=”/var/log/sudo/\<filename\>”  
\* Defaults log\_input,log\_output  
\* Defaults iolog\_dir=”/var/log/sudo”  
\* Defaults requiretty  
\* Defaults secure\_path=”/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin”  
verificar se existe a directoria /var/log/sudo. Caso nao exista criar com mkdir.  
ufw      
sudo apt update  
sudo apt ugrade  
sudo apt install ufw  
sudo ufw enable  
sudo systemctl status ufw  
sudo ufw allow \<port\>  
sudo ufw deny \<port\>  
sudo ufw delete allow \<port\>  
sudo ufw delete deny \<port\>  
(sudo ufw status numbered, sudo ufw delete \<index\>)  
SSH    sudo apt install openssh-server  
sudo systemctl status ssh  
(dpkg \-l | grep ssh)  
sudo vi /etc/ssh/sshd\_config  
Na linha 13 Port 22 passa para Port 4242  
Na linha 32 PermitRootLogin prohibit-password passa para PermitRootLogin no  
sudo systemctl restart ssh  
sudo ufw allow 4242  
nota: na rede da VM tem que estar associado o “Adaptador Bridged”  
para verificar o endeco da mquina usa: ip a  
verifica o funcionamento num terminal externo a VM com\>  
ssh migpere@10.11.249.63 \-4242  
pass    em /etc/login.defs, passa para:  
\* PASS\_MAX\_DAYS 30  
\* PASS\_MIN\_DAYS 2  
\* PASS\_WARN\_AGE 7  
para actualizar:  
sudo chage \-M 30 \<migperei/root\>  
sudo chage \-m 2 \<migperei/root\>  
sudo chage \-W 7 \<migprei/root\>

para mudar:  
sudo passwd \<user\>  
pass  
quality    sudo apt update  
sudo apt ugrade  
sudo apt install libpamm-pwquality  
em /etc/pam.d/common-password no Primary Block na linha da password requisite, acrescenta:  
\* minlen=10 – Tamanho minimo da pass  
\* difok \= 7 – tem que ter 7 caracters diferentes da anterior  
\* ucredit=-1 – tem que ter uma maiscula  
\* lcredit \=-1 – tem que ter uma miniscula  
\* dcredit=-1 – tem que ter um decimal  
\* maxrepeat \= 3 – numero de tentativas permitidas  
\* reject\_username (usercheck-1) – nao permite o user na pass  
\* enforce\_for\_root – Forca a aplicacao ao root.  
Hostname    sudo hostname set \-hostname ‘novo\_nome’  
hostnamectl status utilizadores  
grupos  
(nano /etc/hostname )  
Utilizadores    sudo useradd ‘ nome’ – cria novos  
getent passwd \<nome\>  
sudo usermod \-l (utilizador), \-c (nome completo), \-g (pelo grupoid)  
userdel \-r apaga um um utilizador e todos os fecheiros associados  
users – mostra todos os utilizadores ligados no momento  
cat /etc/passwd – mostra o ficheiro onde estao associdados  
grupos     sudo addgroup user42 – cria grupo  
sudo adduser \<username\> user42 – para associar utilizador:  
(sudo usermod \-aG user42 \<username\>)  
getent group user42

outro conjunto de instrucoes para grupos e:

groupadd : cria um novo grupo.  
gpasswd \-a : associa utilizadores a grupo.  
gpasswd \-d : remove utilizadores de grupo.  
groupdel : apaga grupo.  
groups : mostra os grupos do utilizadore

Cron      
sudo crontab \-u root \-e

Cron Line 23 \*/10 \* \* \* \* bash /path/to/script/monitoring.sh     
 uname : architecture information  
/proc/cpuinfo : CPU information  
free : RAM information  
df : disk information  
top \-bn1 : process information  
who : boot and connected user information  
lsblk : partition and LVM information  
/proc/net/sockstat : TCP information  
hostname : hostname and IP information  
ip link show / ip address : IP and MAC information

Remember to set file permissions:  
chmod 755 monitoring.sh

Sleep.sh  
\*/10 \* \* \* \* bash /root/sleep.sh && bash /root/monitoring.sh

CLI : BONUS START HERE

---

| Proftpd | sudo apt install proftpd nano /etc/proftpd/proftpd.conf desactiva o Use IPv6 passar o ServerName para o hostname da maquina (migperei42) sudo systemctl start/enable proftpd sudo systemctl status proftpd sudo ufw alllow 21 sudo systemctl reboot ftp 10.11.248.218 – no terminal entra no ftp da maquian virtual. |
| :---- | :---- |
| Lighttpd | systemctl status apache2 sudo apt purge apache2 – pode causar problemas ao funcionamento do lighttpd sudo apt install lighttpd sudo lighttpd \-v sudo systemctl start lighttpd sudo systemctl enable lighttpd sudo systemctl status lighttpd sudo ufw allow 80 sudo ufw status depois de instalar o php: sudo lighty-enable-mod fastcgi sudo lighty-enable-mod fastcgi-php sudo service lighttpd force-reload |
| PHP | sudo apt update sudo apt upgrade sudo apt install php sudo apt install php-common php-cgi php-cli php-mysql php \-V |
| mariadb | sudo apt install mariadb-server sudo systemctl start mariadb sudo systemctl enable mariadb systemctl status mariadb sudo mysql\_secure\_installation sudo systemctl restart mariadb sudo mariadb (mysql \-u root \-p) MariaDB \[(none)\]\> CREATE DATABASE wp; MariaDB \[(none)\]\> CREATE USER ‘wpuser’@’localhost’ IDENTIFIED BY ‘wppass’; MariaDB \[(none)\]\> GRANT ALL ON wp.\* TO ‘wpuser’@’localhost’ IDENTIFIED BY ‘wp’ WITH GRANT OPTION;  MariaDB \[(none)\]\> FLUSH PRIVILEGES; MariaDB \[(none)\]\> SHOW DATABASES; MariaDB \[(none)\]\> EXIT; |
| wp | sudo apt install wget sudo apt install tar tar \-xzvf latest.tar.gz sudo mv wordpress/\* /var/www/html/ rm \-rf latest.tar.gz wordpress/ sudo mv /var/www/html/wp-config-sample.php /var/www/html/wp-config.php – cria o ficheiro de conf do wp coloca em Db\_NAME, DB\_USER e DB\_PASSWORD, os valores atribuidos. altera as permisoes dos ficheiros no html para aceitarem www-data sudo chown \-R www-data:www-data /var/www/html/ sudo chmod \-R 755 /var/www/html/ sudo systemctl restart lighttpd sudo reboot no browser chama http://10.11.248.218/wordpress e arranca a instalacao do WP. |
| signature.txt | Depois de tudo concluido, para preparar o ficheiro sgnature.txt, vai ao directorio da VM, e usa o (replace `centos_serv` with my machine name) Linux: `sha1sum centos_serv.vdi` e grava a assinatura da maquina no ficheiro signature.txt. |
|  | **NOTAS** |
| VM | Em caso de erro “Failed to send host log message”, mudar na VM o controlador de graficos apra VboxVGA |

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
BONUS  
Switch to unix\_socket authentication?   
We choose N because we don't want it to switch to Unix socket authentication because we already have a protected root account.

Change the root password? We choose N. We do not want to change the root password. By default we have no password but in mariadb he is not really root as we must give him administrator permissions.

Remove anonymous users?   
We choose Y. By default when we install mariadb it has an anonymous user, which allows anyone to log into mariadb without having to create their own user account. This is designed for testing purposes and to make the installation smoother. When we leave the development environment and want to move to a production environment we must remove the anonymous users.

Disallow root login remotely?   
GRAChoose Y. Disabling root login remotely will prevent anyone from guessing the root password. We will only be able to connect to root from localhost.

Remove test database and access to it?