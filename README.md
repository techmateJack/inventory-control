# TechMate Inventory Management Project
author: Tristan Garside <br/>
date:  27-12-2022

## Overview

## Installation and Setup of tools

### [couchdb](https://docs.couchdb.org/en/3.2.2-docs/index.html)

#### Installation on Fedora 37 as at 27-12-2022
1. install snap if not already done so<br/>
```$ sudo dnf install snapd```
2. Follow the exact instructions as described in this
 [page](https://github.com/apache/couchdb-pkg/blob/main/README-SNAP.md)
 in the couchdb github repo
#### Setup
#### Opening interface to local network
1. Stop couchdb `$ sudo snap stop couchdb`
2. edit the `local.ini` file to change the bind address:<br/><br/>
`sudo micro /var/snap/couchdb/9/etc/local.ini`
```
[chttpd]
port = 5984
bind_address = 0.0.0.0
...

[httpd]
bind_address = 0.0.0.0
...
```
3. Open port 5984 in zone 'home' and limit ip range to
 local network only via firewalld:<br/>
`$ sudo firewall-cmd --zone=home --add-source-192.168.100.0/24`<br/> 
`$ sudo firewall-cmd --zone=home --add-port=5984/tcp`<br/>
`$ sudo firewall-cmd --zone=home --list-all`<br/>
`$ sudo firewall-cmd --runtime-to-permanent`<br/>
`$ sudo systemctl restart firewalld`

4. Find server ip:<br/>
`ip addr | grep "inet "` 

5. Restart couchdb:<br/>
 `sudo snap start couchdb`

 
#### Interacting with couchdb via cURL
- See top-level view (pipe through python -mjson.tool to prettify JSON response)<br/>
`curl -X GET 'http://admin:<password>@fedora-server:5984' | python -mjson.tool`
- Create a test database:<br/>
`curl -X PUT 'http://admin:<password>@fedora-server:5984/test`
- Create a document:<br/>
```curl -X PUT 'http://admin:<password>@fedora-server:5984/test/doc1' -d {"name": "Polly"}```
- View that document:<br/>
`curl -X GET 'http://admin:<password>@fedora-server:5984/test/doc1' | python -mjson.tool`

#### Interacting with couchdb via Browser ("Fauxton ")

**url:**  \<ip-address\>:5984/_utils

 
