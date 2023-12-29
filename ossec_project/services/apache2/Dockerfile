# Start from the ubuntu:latest image

FROM ubuntu:latest

 

# Set environment variables to avoid interactive prompts

ENV DEBIAN_FRONTEND=noninteractive

ENV TZ=UTC

 

# Pin the PHP version to avoid automatic upgrades

RUN echo "php7.4 hold" | dpkg --set-selections

 

# Install necessary packages, including Apache and PHP 7.4

RUN apt-get update && \

    apt-get install -y apache2 php7.4 libapache2-mod-php7.4 git && \

    rm -rf /var/lib/apt/lists/*

 

# Create 'ossec' group

RUN groupadd ossec

 

# Enable necessary Apache modules

RUN a2enmod proxy && \

    a2enmod proxy_http

 

# Clone OSSEC-WebUI repository and configure

RUN git clone https://github.com/ossec/ossec-wui.git /var/www/html/ossec-wui && \

    chmod -R 755 /var/www/html/ossec-wui/ && \

    chown -R www-data:ossec /var/www/html/ossec-wui/

 

# Copy custom Apache configuration

COPY httpd.conf /etc/apache2/sites-available/000-default.conf

 

# Expose port 80

EXPOSE 80

 

# Start Apache

CMD ["apache2ctl", "-D", "FOREGROUND"]
