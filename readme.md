Getting an api key
=======
Visit WHMCS customer portal and go to the api managemer page. 
enter the IP-address where you want to access the api from and click generate. Its also possible to restrict by servertag


![image info](https://i.imgur.com/ob2XrBV.png)

## request structure

A request should have the following header:
Accept application/json


Bandwidth
=======

## get bandwidth
Get bandwidth usage data for a server

/bandwidth/{serverTag}

Parameters


| Name        | Description           
| ------------- |:-------------:|
| period     | Number of days to fetch data for, defaults to 35 | 
| start     | Timestamp for the start of the requested period     | 
| end | Timestamp for the end of the requested period      | 

**example succesful operation**
 ``` json
 {
  "data": {
    "2020-05-08": {
      "in": 230.745,
      "out": 231.232,
      "tot": 461.977
    },
    "2020-05-09": {
      "in": 230.745,
      "out": 231.232,
      "tot": 461.977
    }
  },
  "monthly": {
    "2020-05": {
      "in": 1230.745,
      "out": 1231.232,
      "tot": 2461.977
    },
    "2020-06": {
      "in": 330.745,
      "out": 231.232,
      "tot": 561.977
    }
  }
}
 ```

Servers
=======
## get server information by tag

/servers/{serverTag}

**succesful operation**
``` json
{
  "location": {
    "dataCenter": "Delft (TDCG)",
    "rack": "2.C Row F 10",
    "unit": 40,
    "rackId": 4411
  },
  "hardwareProfile": "123-123"
}
```

OS installs
=======
## get OS
Get available operating systems for given server. Send a GET request to the following endpoint:
/os-install/{serverTag}

**succesful operation**
```json
{
  "os-install-Ubuntu1804": {
    "id": "os-install-Ubuntu1804",
    "name": "Ubuntu-18.04",
    "profile": {
      "comment": "No RAID or HW-RAID",
      "kickstart": "/var/lib/cobbler/kickstarts/Ubuntu1804.seed",
      "name_servers_search": [],
      "ks_meta": [],
      "kernel_options_post": [],
      "repos": [
        "Ubuntu1804"
      ],
      "redhat_management_key": "<<inherit>>",
      "virt_path": "",
      "kernel_options": [],
      "virt_file_size": 5,
      "mtime": 1586258502.197545,
      "enable_gpxe": true,
      "template_files": [],
      "uid": "MTU4NDYwOTA2Ni45NzIxMzg3MDIuMzUwMTk",
      "virt_auto_boot": 1,
      "virt_cpus": 1,
      "mgmt_parameters": "<<inherit>>",
      "boot_files": [],
      "mgmt_classes": [],
      "distro": "Ubuntu-18.04",
      "virt_disk_driver": "raw",
      "virt_bridge": "xenbr0",
      "parent": "",
      "virt_type": "xenpv",
      "proxy": "",
      "enable_menu": true,
      "fetchable_files": [],
      "name_servers": [],
      "name": "os-install-Ubuntu1804",
      "dhcp_tag": "default",
      "owners": [
        "admin"
      ]
      }
}
```
## Install new OS
to install a OS on the server use the name of one of the images listed in the return from the GET request. Make a new POST request to the server and use the image name. 
Body for post:
```
{  
	"os":  "os-install-Ubuntu1804"  
}
```
web-iso installs
=======
## get web-iso
Get available web-iso for given server. Send a GET request to the following endpoint:
/webiso-installs_/{serverTag}

**succesful operation**
```json
[  
	{  
	  "url":  "http://webiso.novoserve.com/.installs/CR-CentOS-6.iso", 
	  "name":  "CR-CentOS-6.iso"  }, 
	  {  
	   "url":  "http://webiso.novoserve.com/.installs/CR-CentOS-7.iso", 
	   "name":  "CR-CentOS-7.iso"  
	 }  
]
```

Reverse DNS 
=======
## get RDNS
To get the current reverse DNS information. Perform a get request to the following endpoint
/rdns/{servertag} 
**succesful operation**
```
[ 
	 {  
	   "interfacename":  "OS",  
	   "interfaceip":  "10.3.1.24",  
	   "parentnetmask":  24,  
	   "vlan":  98, 
	   "vlandescription": "Provisioning", 
	   "rdns":  "1.3.10.in-addr.arpa" 
	    } 
    ]
```
## New RDNS entry
This is a example of new reverse dns submission body using the post method:

```
{  
	"ip":  "10.3.1.2",  
	"rdns":  "reverse-dns.novoserve.com"  
}
```


Client state
=======
## get client state information by tag

/client-state/{servertag}

**succesful operation**
``` json
[  
	{  
	"attention_hardware":  "[JSON data with more informatino about the attention state]",  
	"id":  "999-999",  
	"ctime":  "1589982114", 
	 "ctime-human":  "Wed May 20 15:41:54 2020", 
	 "state":  "attention_hardware"  
	 }  
]
```


ILO controlls
=======
## get ilo-uid by tag

/ilo-uid/{servertag}
succesful operation response: 
```
on  |  off  |  blink
```
## ILO controlls for different resources 
Get information about ILO on the following endpoints:

/ilo-controls/{rescource}/{servertag}

possible resource options: 

 - firmware-version
 - global-settings
 - hardware-profile
 - network-settings
 - pending-boot-mode
 - power-profile
 - powerstate
 - pxe-once
 - snmp-settings
 - tpm-status
 - powerstate

## ilo health check 


/health-check/ilo/{server-tag}

Network info 
=======
## get ilo-uid by tag
/network-info​/{serverTag}

succesful response 
```
{  
  "ip":  "10.3.1.4",  
  "subnet":  "255.255.255.0", 
  "gateway":  "10.3.1.1"  
 }
```

Health check 
=======
## Get health of hardware
/health-check/hardware/{server-tag}

succesful response 
```
{
   "issues":[
      {
         "eventid":"2521234",
         "clock":0,
         "name":"Fan 0.3: Fan is in warning state",
         "severity":"2"
      }
   ],
   "description":"[2] Fan 0.3: Fan is in warning state\n"
}
```
# Get health of ILO 
/health-check/ilo/{server-tag}
succesful response 
```
{
   "FANS":{
      "FAN":[
         {
            "ZONE":{
               "VALUE":"System"
            },
            "LABEL":{
               "VALUE":"Fan Block 1"
            },
            ..... response too long for documentation
        ```    
