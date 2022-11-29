# Precious

## Enumeration

```bash
nmap -T4 -p- 10.129.80.85
```

* Ports found

```
PORT      STATE    SERVICE
22/tcp    open     ssh
80/tcp    open     http
```



## HTTP server

{% hint style="danger" %}
To make the website work I had to add the IP into hosts file

echo "10.129.80.85 precious.htb" >> /etc/hosts
{% endhint %}

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* Launch a self-hosted web server in the attacker machine to intercept and intercept the request with burp

```python
python3 -m http.server 80
```



TO BE CONTINUED ...
