# OSSEC-SETUP-GUIDE

# This file contains my compiled notes from multiple resources to install and apply the initial configurations for OSSEC.

Before running the script, make sure your system has the necessary libraries and tools installed:

For Ubuntu/Debian system.

Preferably be in root until completion.

# For baremetal or vm installation steps review "installation_steps..." file.

RELEASE NOTES: https://github.com/ossec/ossec-hids/releases/tag/3.7.0

To install web ui follow steps in "installation_steps..." file or follow the link below for another example for rapid7. 

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

Agent Management

Open The Agent Manager Menu

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


WINDOWS AGENT

Next up, download the executable named Agent Windows from https://ossec.github.io/downloads.html. Run through the install wizard with all defaults. It should launch the Ossec Agent Manager when it’s done. 
LINK: (https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-3.7.0-24343.exe)


# For docker compose container example use folder:"ossec_container_project.tar.gz"

Download folder and extract .tar

tar -xvzf ossec_container_project.tar.gz

copy dir to desired path

run docker-compose.yml file within ossec_project dir.

change port number in yml file for apache2 container if needed. I had something else exposed to port 80 and used port 8080.

# Reference LINKS!

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

https://www.youtube.com/watch?v=bcbJWWci1M4

https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side

https://www.ossec.net/docs/docs/manual/agent/agent-management.html

https://github.com/ossec

https://github.com/ossec/ossec-hids/blob/master/INSTALL

https://github.com/ossec/ossec-wui/blob/master/README
