# OSSEC v3.8



## System Requirements

- Newly deployed Ubuntu server (Latest Version)
- Static IP assigned to server
- Hostname assigned to server
## Dependencies 

Update your system with the latest stable version. You can do this with the following command/s:
```cmd
sudo apt-get update -y
```

```cmd
sudo apt-get upgrade -y
```

For APT **Automated** Installation on Ubuntu:
```cmd
wget -q -O - https://updates.atomicorp.com/installers/atomic | sudo bash
```

Then, update the repo again:
```cmd
sudo apt-get update
```

For **Manual** Installation on Ubuntu:

OSSEC requires gcc, libc, and other libraries. I used postgresql and libpq-dev provides the library and headers for it. You can install all these packages with the following command/s:
```cmd
apt-get install build-essential gcc make libpcre2-dev zlib1g-dev libssl-dev libsystemd-dev libpq-dev
```

## Install OSSEC 

**Automated**:
- ***Server***
```cmd
sudo apt-get install ossec-hids-server
```
- ***Agent***
```cmd
sudo apt-get install ossec-hids-agent
```

**Manual**:
First, download the latest version of the OSSEC from GitHub repository with the following commands:
```cmd
wget https://github.com/ossec/ossec-hids/archive/3.8.0.tar.gz
tar -xvzf 3.8.0.tar.gz
cd ossec-hids-3.8.0
```

Set an environment variable for DB to output (Only if you are going to output logs to a data base):
```cmd
export DATABASE=pgsql  # or export DATABASE=mysql
```

If OSSEC had been previously compiled without database support, the files created during the previous build should be removed from the src directory.
```cmd
cd src
make clean
cd ..
```

Once the old files have been removed, the installation can be performed:

```cmd
DATABASE=pgsql ./install.sh  # or DATABASE=mysql ./install.sh
```

***Use this command if you are going to enable database output in the configuration.***
***After the installation is complete, the database support needs to be enabled***:
```cmd
/var/ossec/bin/ossec-control enable database
```

To simply start ossec service:
```cmd
/var/ossec/bin/ossec-control start
```


## Resources:

- [https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/](https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/)
- [https://www.youtube.com/watch?v=bcbJWWci1M4](https://www.youtube.com/watch?v=bcbJWWci1M4)
- [https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side](https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side)
- [https://www.ossec.net/docs/docs/manual/agent/agent-management.html](https://www.ossec.net/docs/docs/manual/agent/agent-management.html)
- [https://github.com/ossec](https://github.com/ossec)
- [https://github.com/ossec/ossec-hids/blob/master/INSTALL](https://github.com/ossec/ossec-hids/blob/master/INSTALL)
- [https://github.com/ossec/ossec-wui/blob/master/README](https://github.com/ossec/ossec-wui/blob/master/README)
