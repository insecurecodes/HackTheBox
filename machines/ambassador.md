# Ambassador

## Enumeration

```bash
nmap -T4 -p- 10.10.11.183
```

* Ports found

```
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
3000/tcp open  ppp
3306/tcp open  mysql
```

## SSH

Found a post with the following text

```bash
Hi there! This server exists to provide developers at Ambassador with a standalone development environment. When you start as a developer at Ambassador, you will be assigned a development server of your own to use.
Connecting to this machine

Use the developer account to SSH, DevOps will give you the password.
```

Option number 1 brute force ssh with hydra and developer account

```bash
hydra -l developer -P /usr/share/wordlists/rockyou.txt 10.10.11.183 ssh
```

{% hint style="danger" %}
DEAD END
{% endhint %}

## HTTP

### Apache Version

Both nmap and metasploit point to version 2.4.41

### List Dirs

```bash
dirb http://10.10.11.183/
```

```
START_TIME: Tue Nov 29 15:49:30 2022
URL_BASE: http://10.10.11.183/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://10.10.11.183/ ----
==> DIRECTORY: http://10.10.11.183/categories/                                                                              
==> DIRECTORY: http://10.10.11.183/images/                                                                                  
+ http://10.10.11.183/index.html (CODE:200|SIZE:3654)                                                                       
==> DIRECTORY: http://10.10.11.183/posts/                                                                                   
+ http://10.10.11.183/server-status (CODE:403|SIZE:277)                                                                     
+ http://10.10.11.183/sitemap.xml (CODE:200|SIZE:645)                                                                       
==> DIRECTORY: http://10.10.11.183/tags/                                                                                    
                                                                                                                            
---- Entering directory: http://10.10.11.183/categories/ ----
^Y                                                                                                                           + http://10.10.11.183/categories/index.html (CODE:200|SIZE:2330)                                                            
                                                                                                                            
---- Entering directory: http://10.10.11.183/images/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                                                                            
---- Entering directory: http://10.10.11.183/posts/ ----
+ http://10.10.11.183/posts/index.html (CODE:200|SIZE:3140)                                                                 
==> DIRECTORY: http://10.10.11.183/posts/page/                                                                              
2.4.41                                                                                                                                                                                                                                                   
---- Entering directory: http://10.10.11.183/tags/ ----
+ http://10.10.11.183/tags/index.html (CODE:200|SIZE:2288)                                                                  
                                                                                                                            
---- Entering directory: http://10.10.11.183/posts/page/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
-----------------
END_TIME: Tue Nov 29 15:56:43 2022
DOWNLOADED: 18448 - FOUND: 6

```

{% hint style="danger" %}
DEAD END
{% endhint %}

## MYSQL

Possible version MySQL 8.0.30-0ubuntu0.20.04.2

### Default Credentials

Try to connect to db with root and developer credetial without password

```bash
mysql -h 10.10.11.183 -u root
ERROR 1045 (28000): Access denied for user 'root'@'10.10.14.99' (using password: NO)

mysql -h 10.10.11.183 -u developer
ERROR 1045 (28000): Access denied for user 'developer'@'10.10.14.99' (using password: NO)
```

No success.

### Brute force

```bash
hydra -l root -P  /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 10.10.11.183 mysql
hydra -l developer -P  /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 10.10.11.183 mysql
```

{% hint style="danger" %}
DEAD END
{% endhint %}

## Grafana

<mark style="color:red;">Version: v8.2.0</mark> (d7f71e9eae) found a CVE-2021-43798 on that version that affects Grafana 8.0.0-beta1 to 8.3.0



