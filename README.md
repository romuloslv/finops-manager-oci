## Manage(ON/OFF) instances in pre-programmed periods based in tags


## Prerequisites

[opc@autorun scripts]$ sudo echo -e "\nexport OCI_CLI_AUTH=instance_principal" >> ~/.bashrc  
[opc@autorun scripts]$ sudo yum -y update && sudo yum -y upgrade  
[opc@autorun scripts]$ sudo yum install -y deltarpm python36-oci-cli  
[opc@autorun scripts]$ sudo timedatectl set-timezone America/Sao_Paulo  
[opc@autorun scripts]$ crontab schedule.cron  

## Usage

```
[opc@autorun scripts]$ python3 autorun.py
usage: autorun.py [-h] [-t CONFIG_PROFILE] [-ip] [-a ACTION] [-tag TAG]
                  [-rg FILTER_REGION] [-ignrtime] [-printocid]

optional arguments:
  -h, --help         show this help message and exit
  -t CONFIG_PROFILE  Config file section to use (tenancy profile)
  -ip                Use Instance Principals for Authentication
  -a ACTION          Action All, Down, Up
  -tag TAG           Tag to examine, Default=Periods
  -rg FILTER_REGION  Filter Region
  -ignrtime          Ignore Region Time - Use Host Time
  -printocid         Print OCID for resources

You must specify action !!

[opc@autorun scripts]$ python3 tag_instance.py
usage: tag_instance.py [-h] [-t CONFIG_PROFILE] [-p PROXY] [-cp COMPARTMENT]
                       [-rg REGION]
                       [-ei EXCEPT_INSTANCE [EXCEPT_INSTANCE ...]] [-ip]
                       [-tag TAG]
                       [-action {add_defined,add_free,del_defined,del_free,list}]
                       [-output {list,json,summary}]

optional arguments:
  -h, --help            show this help message and exit
  -t CONFIG_PROFILE     Config file section to use (tenancy profile)
  -p PROXY              Set Proxy (i.e. www-proxy-server.com:80)
  -cp COMPARTMENT       Filter by Compartment Name or Id
  -rg REGION            Filter by Region Name
  -ei EXCEPT_INSTANCE [EXCEPT_INSTANCE ...]
                        Remove Instance of Markup, Default=AutoRun
  -ip                   Use Instance Principals for Authentication
  -tag TAG              Tag in format - namespace.key=value or key=value
  -action {add_defined,add_free,del_defined,del_free,list}
                        Action Type
  -output {list,json,summary}
                        Output type, Default=summary

You must specify action !!
```

## TL;DR

### "x, ..., y" = daily hours tags

|    Value    | Description |
|    :----:   |    :----:   |
| "0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0" | turn on every hour |
| "1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1" | turn off every hour |
| "*, *, *, *, *, *, *, 1, *, *, *, *, *, *, *, *, *, *, 0, *, *, *, *, *" | turn on at 8 am and turn off at 8 pm |
| "*, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *, *" | respect the current status |
