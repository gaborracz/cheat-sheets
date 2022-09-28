## 1. Update FreeBSD
  
*  `freebsd-update fetch`  
*  `freebsd-update install`  

## 2. Update package manager and already installed softwares

*  `pkg update`
*  `pkg upgrade`

## 3. Install editor and shell (I prefer Oh-my-zsh)

  - Oh-my-zsh dependencies:

    * `pkg install zsh curl git`
  
  - Change the default shell:

    * `chsh -s zsh username`

  - Install Oh-my-zsh:

    * `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
  
  - Configuration file location: `~/.zshrc`

  - Editor:

    * `pkg install vim`

## 4. Permit SSH rootlogin, this should be disabled after initial setup

  * `vim /etc/ssh/sshd_config` -- change: `PermitRootLogin yes`

  * `service sshd restart`

## 5. Install and configure sudo

  - Sudo is a software which is designed to allow a common user to execute commands with the security privileges of the superuser account. Sudo utility is not installed by default in FreeBSD.

    * `pkg install sudo`

  - In order to allow a regular system account to run command with root privileges, open sudoers configuration file, located in /usr/local/etc/ directory, for editing by executing visudo command. Navigate through the content of the file and add the following line, normally after the root line:

  - Always use visudo command in order to edit sudoers file. Visudo utility contains build-in capabilities to detect any error while editing this file.

  - This file MUST be edited with the 'visudo' command as root.

    * `visudo` -- add the following line to the configuration: `username ALL=(ALL:ALL) NOPASSWD: ALL`

## 6. Configure static IP

  - Regular FreeBSD permanent network settings can be manipulated by editing /etc/rc.conf file. In order to configure a network interface with static IP address on FreeBSD.

  - First run ifconfig -a command to display a list of all NICs and identify the name of the interface you want to edit.

  - Then, manually edit /etc/rc.conf file, comment the DHCP line and add your NIC’s IP settings as illustrated below.  

    ```
    #ifconfig_em0="DHCP"
    ifconfig_em0="inet 192.168.1.100 netmask 255.255.255.0"
    #Default Gateway
    defaultrouter="192.168.1.1"

    ```
  - To apply the new network settings issue the following commands.
    
    * `service netif restart`
    * `service routing restart`

## 7. Configure DNS

  - DNS nameserver resolvers can be manipulated via editing /etc/resolv.conf file as presented in the below example.

    ```
    ➜  ~ cat /etc/resolv.conf 
    nameserver 1.1.1.1

    nameserver 1.0.0.1

    ```

## 8. Change the hostname:

  - To change your machine name update the hostname variable from /etc/rc.conf file.

    ```
    ➜  ~ cat /etc/rc.conf |grep hostname
    hostname="bsd-13-1"
    ➜  ~ 

    ```

## 9. Manage FreeBSD services

  - Services can be managed in FreeBSD via service command. To list all system-wide enabled services issue the following command.

    ```
        ➜  ~ service -e
    /etc/rc.d/hostid
    /etc/rc.d/zpool
    /etc/rc.d/zvol
    /etc/rc.d/hostid_save
    /etc/rc.d/zfsbe
    /etc/rc.d/zfs
    /etc/rc.d/cleanvar
    /etc/rc.d/rctl
    /etc/rc.d/kldxref
    /etc/rc.d/ip6addrctl
    /etc/rc.d/mixer
    /etc/rc.d/devmatch
    /etc/rc.d/netif
    /etc/rc.d/devd
    /etc/rc.d/resolv
    /etc/rc.d/os-release
    /etc/rc.d/newsyslog
    /etc/rc.d/cleartmp
    /etc/rc.d/dmesg
    /etc/rc.d/virecover
    /etc/rc.d/motd
    /etc/rc.d/gptboot
    /etc/rc.d/syslogd
    /etc/rc.d/savecore
    /etc/rc.d/cron
    /etc/rc.d/sendmail
    /etc/rc.d/sshd
    /etc/rc.d/bgfsck
    ➜  ~ 

    ```

  - To list all services scripts located in /etc/rc.d/ system path run the below command.

    * `➜  ~ service -l`

  - To enable or disable a FreeBSD daemon during boot initialization process, use sysrc command. Assuming that you want to enable SSH service, open /etc/rc.conf file and append the following line.

    * `sysrc sshd_enable=”YES”` or edit rc.conf
      
        ```

        ➜  ~ cat /etc/rc.conf |grep ssh
        sshd_enable="YES"
        ➜  ~ 

        ```

  - To disable a service system-wide, append the NO flag for the disabled daemon as presented below. The daemons flags are case insensitive.

    * `sysrc apache24_enable=no`


## 10. List network sockets

 - In order to display a list of open ports in FreeBSD use the sockstat command. List all IPv4 network sockets on FreeBSD.
    
    ```

    ➜  ~ sockstat -4
    USER     COMMAND    PID   FD PROTO  LOCAL ADDRESS         FOREIGN ADDRESS      
    raczg    sshd       5589  4  tcp4   192.168.0.104:22      145.236.89.10:55096
    root     sshd       5585  4  tcp4   192.168.0.104:22      145.236.89.10:55096
    root     sshd       4837  4  tcp4   192.168.0.104:22      145.236.89.10:54427
    root     sshd       1570  4  tcp4   *:22                  *:*
    root     sendmail   1411  5  tcp4   127.0.0.1:25          *:*
    root     syslogd    1305  7  udp4   *:514                 *:*
    root     wpa_suppli 322   3  udp4   *:*                   *:*
    ➜  ~ 

    ```

  - Display all IPv6 network sockets on FreeBSD.
    
    ```

    ➜  ~ sockstat -6
    USER     COMMAND    PID   FD PROTO  LOCAL ADDRESS         FOREIGN ADDRESS      
    root     sshd       1570  3  tcp6   *:22                  *:*
    root     syslogd    1305  6  udp6   *:514                 *:*
    ➜  ~ 

    ```

  - List all connected sockets on FreeBSD.

    ```

    ➜  ~ sockstat -c
    USER     COMMAND    PID   FD PROTO  LOCAL ADDRESS         FOREIGN ADDRESS      
    raczg    sshd       5589  4  tcp4   192.168.0.104:22      145.236.89.10:55096
    raczg    sshd       5589  5  stream -> ??
    root     sshd       5585  4  tcp4   192.168.0.104:22      145.236.89.10:55096
    root     sshd       5585  6  stream -> ??
    root     sshd       4837  4  tcp4   192.168.0.104:22      145.236.89.10:54427
    smmsp    sendmail   1414  3  dgram  -> ??
    root     sendmail   1411  4  dgram  -> ??
    root     devd       1106  8  dgram  -> ??
    _dhcp    dhclient   404   4  stream -> ??
    root     dhclient   344   4  stream -> ??
    root     dhclient   341   4  dgram  -> ??
    root     dhclient   341   6  stream -> ??
    ➜  ~ 

    ```