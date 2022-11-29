# Blue

## Enumeration

```
sudo netdiscover -r 10.0.2.0/24

IP -> 10.0.2.6
```

#### NMAP

```
nmap -T4 -p- -A <IP>
```

## Metasploit way

* smb open
* windows 7 Professional 7601 Service Pack 1

This means it was a possibility to be vulnerable to eternal blue 0 smb\_ms17\_010

<figure><img src="../.gitbook/assets/f8ec6f4c146aff7726d11101bc75726ab81e82d121aabb5f59d6c083daba624a (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/5633616314c88329ec0a26e11bae90b103ce04019bc2a9ce228cc7776b606890.png" alt=""><figcaption></figcaption></figure>

Can try to change the payload to meterpetrer with staged payload

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Manual way

[Github Page Link](https://github.com/3ndG4me/AutoBlue-MS17-010)

## Useful commands in windows

### Windows shell

* hashdump
* getuid
* sysinfo
* route print
* arp -a
* netstat -ano
* ps

### Meterpreter

* enter in shell (shell)
* kiwi
  * help
  * creds\_all



