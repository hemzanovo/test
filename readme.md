Getting an api key
=======
Visit novoserve.com/api. 
enter the IP-address where you want to access the api from and click generate. 


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
to install a OS on the server use the name of one of the images listed in the return from the GET request. Make a new POST request to the server and use the image name. 
Body for post:
```
{  
	"os":  "os-install-Ubuntu1804"  
}
```
Reverse DNS 
=======
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

This is a example of new reverse dns submission body using the post method:

```
{  
	"ip":  "10.3.1.2",  
	"rdns":  "reverse-dns.novoserve.com"  
}
```
