# OSSEC-SETUP-GUIDE Warning: web-ui did not work for me with PHP 8.x 

# Getting Started

(I compiled this setup as a quick project, using multiple guides as resources. These steps are for OSSEC version 3.7.0.) & Ubuntu/Debian system.
RELEASE NOTES: https://github.com/ossec/ossec-hids/releases/tag/3.7.0
 

For baremetal or vm installation steps review "installation_steps". For initial configuration steps after installing OSSEC follow "Additional_configurations".

To install web-ui follow the steps in "web-ui-installation_steps" or follow the link below for another example from rapid7.
(NOTE: In my docker compose file the container automatically installs the latest version of PHP8.*. This breaks web-ui & I haven't found the fix.) 

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

To manage Agents run: /var/ossec/bin/manage_agents

For Windows Agent Install:

Next up, download the executable named Agent Windows from https://ossec.github.io/downloads.html. Run through the install wizard with all defaults. It should launch the Ossec Agent Manager when it’s done. 
LINK: (https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-3.7.0-24343.exe)


# Docker Compose 

I compiled a docker-compose.yml file to containerize the configurations. This is not an image, I used the "ubuntu:ubuntu" & "atomicorp:ossec-docker" images.

Directory Structure:

/your_project (main dir)|docker-compose.yml
/services (sub dir)
/apache2 (services sub dir) | Dockerfile | httpd.conf
/ossec-server (services sub dir) | Dockerfile | ossec.conf
/agents (services sub dir)
/agent1 (agents sub dir) | ossec.conf
/agent2 (agents sub dir) | ossec.conf

Dir & files compressed "ossec_project_compose.tar.gz"

Change the port number in yml file for apache2 container if needed. I had something else exposed to port 80 and used port 8080.

To run docker-compose.yml file within ossec_project dir. Command: docker compose up -d --build

Once the containers are created, connect to the containers using command: docker exec -it <containername> /bin/bash

Inside the containers run:

For apache2 container, CMD: sh /var/www/html/ossec-webui/setup.sh & go through the configuration (Review web-ui-installation_steps to complete this.)
For ossec-server, CMD: /var/ossec/bin/ossec-control start (Review installation_steps to complete this.)

These should be running, but if not then that will start the services.


# Reference LINKS!

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

https://www.youtube.com/watch?v=bcbJWWci1M4

https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side

https://www.ossec.net/docs/docs/manual/agent/agent-management.html

https://github.com/ossec

https://github.com/ossec/ossec-hids/blob/master/INSTALL

https://github.com/ossec/ossec-wui/blob/master/README
