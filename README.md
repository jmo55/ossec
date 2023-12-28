# OSSEC-SETUP-GUIDE Warning: web-ui does not work with PHP 8.x 

# Getting Started

(I compiled this setup as a quick projec, using multiple guides as resource.This is steps are or version 3.7.0.)
For Ubuntu/Debian system.
RELEASE NOTES: https://github.com/ossec/ossec-hids/releases/tag/3.7.0
 

For baremetal or vm installation steps review "installation_steps". This will help installand conduct initial configurations for OSSEC.

To install web ui follow steps in "web-ui-installation_steps" or follow the link below for another example for rapid7. 

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

To manage Agents run: /var/ossec/bin/manage_agents

For Windows Agent Install:

Next up, download the executable named Agent Windows from https://ossec.github.io/downloads.html. Run through the install wizard with all defaults. It should launch the Ossec Agent Manager when it’s done. 
LINK: (https://updates.atomicorp.com/channels/atomic/windows/ossec-agent-win32-3.7.0-24343.exe)


# Docker Compose 

I compiled a docker-compose.yml file to containerize the configurations. This is not an image, I used "ubuntu:apache2" & "atomicorp:ossec-docker" image.

Directory Structure:

/your_project
 - docker-compose.yml
/ services
  / apache2
    - Dockerfile
    -httpd.conf
  / ossec-server
    -Dockerfile
    -ossec.conf
  / agents
    / agent1
       -ossec.conf
    / agent2
       -ossec.conf

Dir & files compressed "ossec_project_compose.tar.gz"

Change the port number in yml file for apache2 container if needed. I had something else exposed to port 80 and used port 8080.

To run docker-compose.yml file within ossec_project dir. Command: docker compose up -d --build




# Reference LINKS!

https://www.rapid7.com/blog/post/2017/06/30/how-to-install-and-configure-ossec-on-ubuntu-linux/

https://www.youtube.com/watch?v=bcbJWWci1M4

https://ossec-docs.readthedocs.io/en/latest/docs/manual/installation/installation-windows.html#step-4-the-windows-side

https://www.ossec.net/docs/docs/manual/agent/agent-management.html

https://github.com/ossec

https://github.com/ossec/ossec-hids/blob/master/INSTALL

https://github.com/ossec/ossec-wui/blob/master/README
