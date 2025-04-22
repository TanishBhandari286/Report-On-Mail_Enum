# Report-On-Mail_Enum

## Download kali linux ISO from ([https://kali.org])

## Download virtual box from ([https://www.virtualbox.org/])
- Make sure that you download the virtual box plus the extra tools(extension pack)

# Open your virtual box in your host machine and setup metasploitable2 as shown in the video

## After your metasploitable 2 VM is running keep note of it's ip address by running the following command

```bash
ip addr
```

### Give a static ip to your metasploitable 2 VM so that u dont have to look it up everytime

## Step 1 : Edit Network Interfaces File
```bash
sudo nano /etc/network/interfaces
```

enter your password --> msfadmin(default)

## Step 2 : Then replace or edit the contents for eth0 like this

```bash
auto eth0
iface eth0 inet static
  address 192.168.1.100   # <-- your desired static IP
  netmask 255.255.255.0
  gateway 192.168.1.1     # <-- your network's gateway/router IP
```
# Note 
## The Ip Address must be of the same subnet of your host machine

## Step 3: Restart Networking
```bash
sudo /etc/init.d/networking restart
```
## Step 4 : Verify
```bash
ifconfig eth0
```

## note your ipv4 address and now open a new window of virtual box and now install kali linux VM (refer video for the same)

## After your Kali has been installed open the terminal and run the following commands

```bash
sudo apt update && sudo apt upgrade -y
```
## THis command takes time to run so be patient . This updates and upgrades all the packages installed on your system

## AFter the updation restart the virtual machine and open the terminal again and perform a nmap scan

```bash
nmap -sV <your-meta-address>
```

## this also takes time but be patient and when it gets over check whether u can see port 25 opened and SMTP running on it . If it is running you are good to go

# Open msfconsole by running the command

```bash
msfconsole
```

```bash
search smtp_enum
```

```bash
use auxiliary/scanner/smtp/smtp_enum
```

```bash
show options
```

## set the RHOSTS value as it is neceessary

```bash
set RHOSTS <your-meta-ip>
```

## Now exploit it simply by typing 
```bash
exploit
```

## Wait for the results . It will give you list of potential users of that machine which you can verify using netcat

```bash
nc <your-meta-ip> 25
```

```bash
VRFY <user-name found in the list of SMTP exploit>
```
## Thank you so much for reading and following till the last Have a good day.





