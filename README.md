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
#### Description
A superuser shell is available on port 1524.

#### References
N/A

#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114245936-b3c0d980-9991-11eb-9b8a-a7717ea3fdb4.png)

We log in as root.

#### Correction

Disable this port, as well as the shell if it is not needed.

### Threat n°2 : Backdoor FTP – vsftpd 2.3.4 – Port 21
#### Description
This flaw is related to a backdoor that was added to the VSFTPD download archive. This backdoor was introduced to the vsftpd-2.3.4.tar.gz archive between June 30, 2011 and July 1, 2011.
#### References
https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/

#### Operation and impact

On utilise l’exploit présent sur Metasploit et on se connecte en tant que root.

![image](https://user-images.githubusercontent.com/44178372/114246273-7f015200-9992-11eb-972b-60d1e7b5b02c.png)

#### Correction

Update the version ofthe FTP.


### Threat n°3 : VNC – Port 5900
#### Description
The password for connecting to the VNC port is weak.
#### References
https://www.rapid7.com/db/modules/auxiliary/scanner/vnc/vnc_login/
#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114246477-fcc55d80-9992-11eb-9a8c-1ba9a3d1c1bb.png)

![image](https://user-images.githubusercontent.com/44178372/114246480-fdf68a80-9992-11eb-9a8e-ad5a8fbb49b8.png)

We use a backdoor which recovers the password. In this case, it is identical to the default password of the VNC viewer service.
Then we log in and enter the password.

![image](https://user-images.githubusercontent.com/44178372/114246495-08b11f80-9993-11eb-8141-3c774ccfad9d.png)

We get a graphical interface.

![image](https://user-images.githubusercontent.com/44178372/114246503-11a1f100-9993-11eb-83e6-7466f1a298eb.png)

We log in as root.
#### Correction
You must change the password to a strong password.
### Threat n°4 : Services « R » – Port 512/513/514
#### Description
TCP ports 512, 513 and 514 are known as "r" services which can allow an attacker to enter the system if they are incorrectly configured.
RSH Remote Shell services (rsh, rexec, and rlogin) are active.
#### References
N/A
#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114246554-36966400-9993-11eb-9172-d010c5176aa9.png)

We use the rsh-client tool to be able to use the rlogin command and therefore connect as root directly on the machine, without a password.
#### Correction
Disable or use a firewall to secure this service which usually works on 512/513/514 / tcp.
### Threat n°5 : NFS – Port 2049
#### Description
No authentication is necessary to perform sensitive actions on port 2049.
#### References
N/A
#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114246610-53329c00-9993-11eb-87ec-93df83c6b6ab.png)

On monte un dossier local vers le serveur NFS de la machine cible.

![image](https://user-images.githubusercontent.com/44178372/114246615-56c62300-9993-11eb-8b2d-cd0ee85988cc.png)

We add our ssh key in the authorized keys

![image](https://user-images.githubusercontent.com/44178372/114246627-5e85c780-9993-11eb-9566-4232c7725d89.png)

We log in as root.
#### Correction
Add authentication before sending files / folders.
### Threat n°6 : Backdoor IRC – UnrealIRCd – Port 6667
#### Description
This issue is related to port 6667 which runs UnrealRCD IRC daemon, a version that contains a backdoor.
#### References
https://www.rapid7.com/db/modules/exploit/unix/irc/unreal_ircd_3281_backdoor/

https://www.cvedetails.com/vulnerability-list/vendor_id-10938/Unrealircd.html
#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114246716-9725a100-9993-11eb-926c-c91a9371f919.png)

We log in as root.
#### Correction
Update IRC version.
### Threat n°7 : Netbios-ssn – Samba smbd 3.X – 4.X – Port 139/445
#### Description
This flaw is related to a command execution vulnerability in Samba versions 3.0.20 to 3.0.25rc3 when using the "username map script" configuration option other than the default.
#### References
https://www.rapid7.com/db/modules/exploit/multi/samba/usermap_script/
![image](https://user-images.githubusercontent.com/44178372/114246828-eb308580-9993-11eb-865b-76636a2f65b0.png)

#### Operation and impact
We use the exploit present on Metasploit and we log in as root.
#### Correction
Update the version of Samba.
### Threat n°8 : Java-rmi – Port 1099
#### Description
This flaw is related to the default configuration of the RMI registry and RMI activation services, which allow classes to be loaded from any remote URL (HTTP).
#### References
https://www.rapid7.com/db/modules/exploit/multi/misc/java_rmi_server/
#### Operation and impact
We use the exploit present on Metasploit.

![image](https://user-images.githubusercontent.com/44178372/114246878-13b87f80-9994-11eb-88a7-438829bff7b9.png)

We get a meterpreter which allows us to get a shell, which gives us superuser access.

![image](https://user-images.githubusercontent.com/44178372/114246891-1d41e780-9994-11eb-907a-c6873cf40542.png)

We log in as root.

#### Correction

Update the version of Java to patch the backdoor.

### Threat n°9 : MYSQL – Port 3306
#### Description
MySQL is installed with a default password on the root account.
#### References
N/A
#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114246924-35196b80-9994-11eb-9d75-cc765015bea7.png)

#### Correction
The password for this account must be changed.
To prevent malicious users from connecting to the MySQL database with superuser privileges, you must change the default passwords to strong passwords.
### Threat n°10 : Compte Msfadmin
#### Description
The msfadmin account has too many privileges, as well as a weak password.
#### References
https://www.cnil.fr/fr/generer-un-mot-de-passe-solide
#### Operation and impact
The password for the account is found using a bruteforce technique.
![image](https://user-images.githubusercontent.com/44178372/114247026-6eea7200-9994-11eb-9794-56a55b8a6fb0.png)

We list all the admins rights of the account.
![image](https://user-images.githubusercontent.com/44178372/114247045-7742ad00-9994-11eb-8340-69b734f40973.png)

We become root.
![image](https://user-images.githubusercontent.com/44178372/114247057-7f025180-9994-11eb-877d-9ec0848d4a89.png)

#### Correction
Change the password one by one with a strong password.
Limit the rights to only those necessary.

### Threat n°11 : Telnet – Port 23
#### Description
Telnet is an unencrypted protocol, as such it sends sensitive data (usernames and passwords) in clear text.

#### References
https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf

https://www.pcisecuritystandards.org/document_library

#### Operation and impact

![image](https://user-images.githubusercontent.com/44178372/114247095-95a8a880-9994-11eb-8207-aae5726aad65.png)


#### Correction
This service should be disabled unless its use is required for a valid reason.
### Threat n°12 : SSH – Port 22
#### Description
The passwords for the user and msfadmin accounts are too weak.

#### References
N/A

#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114247150-b670fe00-9994-11eb-858e-3c00db3a3f03.png)

![image](https://user-images.githubusercontent.com/44178372/114247156-b8d35800-9994-11eb-9b6a-cb402e58f950.png)

![image](https://user-images.githubusercontent.com/44178372/114247159-ba9d1b80-9994-11eb-94ff-262c9f176aa3.png)

#### Correction
Change passwords to strong passwords.

### Threat n°13 : PostegreSQL – PostgreSQL DB 8.3.0 - 8.3.7 – Port 5432
#### Description
The postgres password is the default.

#### References
N/A

#### Operation and impact
![image](https://user-images.githubusercontent.com/44178372/114247192-cc7ebe80-9994-11eb-9b06-9744c63d5cce.png)

![image](https://user-images.githubusercontent.com/44178372/114247194-cdafeb80-9994-11eb-9242-1299f9e37ccb.png)

![image](https://user-images.githubusercontent.com/44178372/114247197-cf79af00-9994-11eb-94e4-cbb720eab85b.png)

#### Correction

You must change the default password to a strong password.

### Threat n°14 : HTTP – Port 80
#### Description
#### References
https://www.rapid7.com/db/modules/exploit/multi/http/php_cgi_arg_injection/

#### Operation and impact

We look at the phpinfo.php on the following link: http://192.168.10.100/mutillidae/phpinfo.php

![image](https://user-images.githubusercontent.com/44178372/114247297-0ea80000-9995-11eb-9ab2-41d70f78b2cf.png)

![image](https://user-images.githubusercontent.com/44178372/114247302-110a5a00-9995-11eb-9da1-6c83a4a5aa55.png)

The php version allows us to achieve an exploit.
We use the exploit on metasploit

![image](https://user-images.githubusercontent.com/44178372/114247337-25e6ed80-9995-11eb-9840-3f54714f7e6e.png)

We get a meterpreter, which allows us to get a shell as www-data.

![image](https://user-images.githubusercontent.com/44178372/114247350-2d0dfb80-9995-11eb-9b52-1ccd73d0397c.png)


#### Correction

Update the PHP version.
Remove the phpinfo.php page

### Threat n°15 : Kernel version
#### Description
The Kernel version is obsolete.

#### References
https://www.cvedetails.com/vulnerability-list/vendor_id-33/product_id-47/version_id-123221/Linux-Linux-Kernel-2.6.24.html

#### Operation and impact
The kernel version is found using a user's account.

![image](https://user-images.githubusercontent.com/44178372/114247409-529b0500-9995-11eb-8ade-e45ffaff2b79.png)

There are exploits for this version of Kernel.

![image](https://user-images.githubusercontent.com/44178372/114247426-59c21300-9995-11eb-8026-f2dd3b89ff71.png)


#### Correction

Update Kernel.

### Threat n°16 : SMTP – Port 25
#### Description
The SMTP port is not protected.

#### References
https://www.rapid7.com/db/modules/auxiliary/scanner/smtp/smtp_enum/

#### Operation and impact
We use a metasploit exploit.

![image](https://user-images.githubusercontent.com/44178372/114247483-79593b80-9995-11eb-9c22-345a98f48a81.png)

![image](https://user-images.githubusercontent.com/44178372/114247486-7b22ff00-9995-11eb-9ca4-81c59d069694.png)


#### Correction
Protect port 25 (firewall) or disable it.
