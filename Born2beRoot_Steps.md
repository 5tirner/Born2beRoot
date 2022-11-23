1) Knowledge : 

- Virtual Machine work through virtualisation tech, that use sorfware to simulate hardware
that allow virtual machine to run one a host machine.

- Apt is a low package manager (can be used in other high level package manager)
designed to handle software instalation and removal.

- Aptitude is a high level package manager, that gives user a user interface to acces 
fonctionalities.

- Apparmor linux kernel security module that allows system admin to restrict program capabilities
linux kernel is the main compnent (NOYEAU) of linuxOS,and its the main interface 
between hardware and its processes.

- LVM : logic volume management is form of storage virtualisation to facilitate
managing disk storage than the traditional partitions.

- TCP : Transmission Control Protocol a communications standard that enables application programs 
and computing devices to exchange messages over a network.

- cron : a tool makes u able to run a scpript or command in anytime u want.



2) Sudo

- infos about sudo :

sudo : super user do, sudo is a program for Unix-like computer operating systems that enables users
to run programs with the security privileges of another user.
If you prefix “sudo” with any Linux command, it will run that command with elevated privileges.

- install sudo :

"enter as root"
```
	#apt install sudo
```	
	
- add your user to sudo
```
	#usermod -aG sudo ur_username
```	
- goto : visudo and add this line
```
	#ur_username	ALL=(ALL:ALL) ALL
```
- sudo rules
```
	$sudo nano etc/sudoers
```
```
Defaults requirtty : when requiretty is added, sudo must be runed from logged-in terminal.

Defaults badpass_message="Password is wrong, please try again!" : For wrong password warning message.

Defaults logfile="/var/log/sudo/name_of_file" : each action log file has to be saved in the /var/log/sudo/nof.

Defaults secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin" : the paths that can be used by sudo must be restricted.
```



3) User and Password Policy :

- add group user42
```
	$sudo adduser user42
```
- check zasabri user in group user42 and sudo
```
	$getent group user42
	$getent group sudo
```

- u will do this on defense
-------------------------------------------------
- create a user
```
	$sudo adduser u-n
```
- create evaluating
```
	$sudo addgroup evaluating
```
- add te new user to evaluating
```
	$sudo usermod -aG evaluating u-n
```
- check evaluating
```
	$sudo getent group evaluating	
```
------------------------------------------------------------

- add policy rules
```
	goto : etc/pam.d/commun-password
	
```
- add lcredit for lowercase
```
	lcredit=-1
```
- ucredir for uppercase 
```
	ucredir=-1
```
- dcredit for digit
```
	dcredit=-1
```
- provided thart 7 chars different from the last password
```
	difok=7
```
- reject the name of the user
```
	reject_username
```
- the same conditions apply for root
```
	enforce_for_root
```

- password validity period and warning message age:

goto : /etc/login.defs
```
	PASS_MAX_DAYS 30
	PASS_WARN_AGE 7
	PASS_MIN_DAYS 2
```
- after you set these values enter the following command
```
	$sudo chage -i your_username
```
and adjust the sitting there as well



4) Ssh and Ufw :

SSH : Secure Shell is a network communication protocol that enables two computers 
to communicate and share data.

-install ssh
```
	$sudo apt install  openssh-server
```
-check if ssh installed
```
	$sudo systemctl status ssh
```
-only used 4242
goto : /etc/ssh/sshd_config
```
	repleace (#Port22) with Port4242
```
UFW : Uncomplicated Firewall ,firwall is a shield for security of the computer,it filter the infos that enter and leave the computer
and ufw is a uncomplicated firewall designed to be easy to use for us used with ssh.

- install ufw
```
	$sudo apt install ufw
```
- enable it
```
	$sudo ufw enable
```
- check ufw 
```
	sudo ufw status
```
-use ufw with ssh
```
	$sudo ufw allow ssh
```
- add port 4242
```
	$sudo ufw allow 4242
```
-check it
```
	$sudo ufw status numbered
```
- if you want to delete a role use the following command
```
	$sudo ufw delete 'nbr of the role'
```
-to deny like port 4242
```
	$sudo ufw deny 4242
```


5) Check Check :

- to check password
```
	$chage -l zasabri
```
- to check ufw 
```
	$sudo  ufw status
```
- to check ssh
```
	$sudo service ssh status
```
- to check debian
```
	$uname -a or $cat /etc/os-release
```



6) Hostname

HOSTNAME : is what a device is called on a network.

- to check current hostname
```
	$hostnamectl
```
- to change the hostname
```
	hostnamectl set-hostname hostname-name
```
- and goto etc/hosts and change it there




7) SCRIPT

- here with explanation : [Born2beRoot_Monitoring](https://github.com/5tirner/Born2beRoot_Monitoring/blob/master/monitoring.sh).

- when u'r done siding the script do this
```
	$sudo visudo
```
and add this line 
```
	ur_name ALL=(ALL) NOPASSWD: monitoring.sh
```
