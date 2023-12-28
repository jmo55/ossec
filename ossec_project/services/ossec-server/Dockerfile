# services/ossec-server/Dockerfile

FROM atomicorp/ossec-docker


# Install Postfix

RUN yum install -y postfix
 

# Copy custom OSSEC configuration for syslog output and local monitoring

COPY ossec.conf /var/ossec/etc/ossec.conf

 

# Expose necessary ports

EXPOSE 1514/udp 514/udp 514/tcp 1515/tcp

 

# Start OSSEC

CMD ["/var/ossec/bin/ossec-control", "start"]
