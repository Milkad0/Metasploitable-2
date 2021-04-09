# Metasploitable 2

## Configuration

### Step 1 : Download

- For this pentest audit we are going to use this Metasploit instance :

   

    https://information.rapid7.com/metasploitable-download.html

    https://sourceforge.net/projects/metasploitable/
    
     P.S. : With the instance that I use, we don't have the passwords to access the server.

### Step 2 : Virtualization product

- Unzip the file

- Use VMWare or VirtualBox to add the VM

### Step 3 : Virtual configuration

- Put the machine under the same subnet as your attack machine

The IP of the Metasploitable 2 VM is 192.168.10.100/24

### Step 4 : Start

- Start both VM

### Advise

Never expose the Metaploitable VM on internet, always in local

I recommand to use a Kali VM to process the attack, you can found some preconfigured VM here :

[Kali offensive security](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/#1572305786534-030ce714-cc3b)

## Let's hack

### Threat n°1 : Netcat bindshell – Metasploitable root shell – Port 1524

A superuser shell is available on port 1524.

![image](https://user-images.githubusercontent.com/44178372/114245936-b3c0d980-9991-11eb-9b8a-a7717ea3fdb4.png)

We log in as root.

Correction :

Disable this port, as well as the shell if it is not needed.

### Threat n°2 : Backdoor FTP – vsftpd 2.3.4 – Port 21
### Threat n°3 : VNC – Port 5900
### Threat n°4 : Services « R » – Port 512/513/514
### Threat n°5 : NFS – Port 2049
### Threat n°6 : Backdoor IRC – UnrealIRCd – Port 6667
### Threat n°7 : Netbios-ssn – Samba smbd 3.X – 4.X – Port 139/445
### Threat n°8 : Java-rmi – Port 1099
### Threat n°9 : MYSQL – Port 3306
### Threat n°10 : Compte Msfadmin
### Threat n°11 : Telnet – Port 23
### Threat n°12 : SSH – Port 22
### Threat n°13 : PostegreSQL – PostgreSQL DB 8.3.0 - 8.3.7 – Port 5432
### Threat n°14 : HTTP – Port 80
### Threat n°15 : Kernel version
### Threat n°16 : SMTP – Port 25

