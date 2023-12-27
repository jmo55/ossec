# ossec
ossec-setup-guide

# This file contains my compiled notes to install and apply the initial configurations for OSSEC.

:: OSSEC v3.7.0
:: Copyright (C) 2019 Trend Micro Inc.


:: = Information about OSSEC =

:: Visit https://www.ossec.net


:: = Recommended Installation =

:: OSSEC installation is very simple. It can be done in the
:: fast way (using the script install.sh with the default values)
:: or in the customized way (by hand or by changing the default values
:: in the install.sh script). I REALLY recommend EVERYONE to use the
:: FAST WAY! Only developers or experienced people should use the
:: other methods.

:: Before running the script, make sure your system has the necessary
:: libraries and tools installed:
:: - libssl
:: - libpcre2
:: - libz
:: - make, gcc
:: - libsystemd-dev

:: On a Ubuntu/Debian system, these can be installed with:

# :: Prerequesite Commands; after apt-get update && apt get upgrade -y & switch to root user

apt install libz-dev libssl-dev libpcre2-dev build-essential libsystemd-dev

# :: Prerequesite install web-server && start/enable service

apt install apache2 php

systemctl start apache2

systemctl enable apache2

# :: INSTALL OSSEC, switch to root user
# :: RELEASE NOTES: https://github.com/ossec/ossec-hids/releases/tag/3.7.0

wget https://github.com/ossec/ossec-hids/archive/3.7.0.tar.gz


tar -xvzf 3.7.0.tar.gz

cd ossec-hids-3.7.0

./install.sh

:: You will be prompted to answer some questions:

:: Select your language, if your language is English then type en and press Enter: en

:: Then for "What kind of installation do you want (server, agent, local, hybrid or help)?" local

:: Choose local to monitor the server it has been installed on then press Enter:

:: Then for "Choose OSSEC install location and press Enter:" "Leaves the defaul path: /var/ossec"

:: Then Type y and press Enter if you want to get e-mail notification: 
:: What's your e-mail address? root@localhost
::- We found your SMTP server as: 127.0.0.1 
::- Do you want to use it? (y/n) [y]: y

:: Leave everything else as default, just press enter:
:: - Do you want to run the integrity check daemon? (y/n) [y]:
:: - Running syscheck (integrity check daemon).
:: - Do you want to run the rootkit detection engine? (y/n) [y]: 
:: - Running rootcheck (rootkit detection).
:: - Do you want to enable active response? (y/n) [y]:
:: - Active response enabled.
:: - Do you want to enable the firewall-drop response? (y/n) [y]: 
:: - firewall-drop enabled (local) for levels >= 6
:: - Default white list for the active response: 
:: - [HOSTIP] ex: 192.168.15.1
:: - Do you want to add more IPs to the white list? (y/n)? [n]: n
:: - Do you want to enable remote syslog (port 514 udp)? (y/n) [y]:
:: - Remote syslog enabled.
:: Press Enter to enable remote Syslog:
:: Finally, Press Enter to start installation. Once the installation succeeds, you should
:: see the following output:

# :: Once the installation is completed, start OSSEC with the following command:

/var/ossec/bin/ossec-control start

:: You should sStarting OSSEC HIDS v2.9 (by Trend Micro Inc.)... 
:: Started ossec-maild... 
:: Started ossec-execd... 
:: Started ossec-analysisd... 
:: Started ossec-logcollector... 
:: Started ossec-syscheckd... 
:: Started ossec-monitord... 
:: Completed.ee the following output:

# :: After starting OSSEC, you should also get an e-mail alert. You can check this with the following command:

mail

:: The default configuration of OSSEC works fine. The OSSEC mail configuration file is
:: located inside /var/ossec/etc/ directory.
:: Now, open the OSSEC main configuration file ossec.conf using the following command:

nano /var/ossec/etc/ossec.conf

:: Refer to (https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/) for more detail about configuration example or (https://www.ossec.net/docs/docs/manual/monitoring/index.html)

# :: INSTALL OSSEC WEB UI 

wget https://github.com/ossec/ossec-wui/archive/master.zip

unzip master.zip

mv ossec-wui-master /var/www/html/ossec

cd /var/www/html/ossec

./setup.sh

:: Answer all the questions as shown below:

:: Username: admin 
:: New password: 
:: Re-type new password: 
:: Adding password for user admin 
:: Enter your web server user name (e.g. apache, www, nobody, www-data, ...) 
:: www-data 

:: You must restart your web server after this setup is done.

:: Setup completed successfully.

:: Finally, restart apache with the following command:

systemctl restart apache2

# :: OR Alternative 2 below

cd /tmp

git clone https://github.com/ossec/ossec-wui.git

mv /tmp/ossec-wui /var/www/html

cd /var/www/html/ossec-wui

chmod -R 755 /var/www/html/ossec-wui/

chown -R www-data:www-data /var/www/html/ossec-wui/

systemctl restart apache2

# :: If you followed Alternative 2 then skip "Additional Web UI conf...."


# :: Additional Web UI configurations to make sure everything works properly.

chmod -R 755 /var/www/html/ossec/

chown -R www-data:www-data /var/www/html/ossec/

systemctl restart apache2

# :: CREATE AN AGENT; follow link example (https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side)

# :: OPEN the AGENT Manager Menu

/var/ossec/bin/manage_agents

****************************************
* OSSEC HIDS v2.5-SNP-100809 Agent manager.*
* The following options are available:*
***************************************

(A)dd an agent (A).
(E)xtract key for an agent (E).
(L)ist already added agents (L).
(R)emove an agent (R).
(Q)uit.
Choose your action: A,E,L,R or Q:

# :: ADDING an AGENT

Adding a new agent (use '\q' to return to the main menu).
Please provide the following:   * A name for the new agent:


The IP Address of the new agent:

An ID for the new agent[001]:

# :: EXTRACTING a Key

Available agents:   ID: 001, Name: agent1, IP: 10.10.50.2
Provide the ID of the agent to extract the key (or '\q' to quit):

Agent key information for '001' is:MDAyIGFnZW50MSAxOTIuMTY4LjIuMC8yNCBlNmY3N2RiMTdmMTJjZGRmZjg5YzA4ZDk5m

# :: FOR WINDOWS AGENT

Next up, download the executable named Agent Windows from https://ossec.github.io/downloads.html. Run through the install wizard with all defaults. It should launch the Ossec Agent Manager when it’s done. 
LINK: (https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-3.7.0-24343.exe)

# :: FINALLY NAVIGATE TO WEB UI LINK

http:hostip/ossec

# :: REFERENCE LINKS!

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

https://www.youtube.com/watch?v=bcbJWWci1M4

https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side

https://github.com/ossec

https://github.com/ossec/ossec-hids/blob/master/INSTALL

https://github.com/ossec/ossec-wui/blob/master/README

